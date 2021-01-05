---
title: flutter中的websocket概念
date: 2021-01-05 11:44:00
tags:
---

目的：实现客户端与服务端的实时通讯，基于TCP协议

与keep-alive区别：keep-alive机制会连接一小段时间，最终会断开，ws协议不会断开

原理：通过一条特殊的http协议请求进行握手后，服务端支持ws协议，则进行协议升级，利用http创建的tcp连接，实现长连接。

步骤分解：

- 连接服务器

  ```dart
  final channel = IOWebSocketChannel.connect('ws://echo.websocket.org');
  ```

  

- 关闭连接

  ```dart
  channel.sink.close();
  ```

  

- 监听服务器

  - StreamBuilder是一个组件，收到一个stream就刷新界面

  ```dart
  new StreamBuilder(
    stream: widget.channel.stream,
    builder: (context, snapshot) {
      return new Text(snapshot.hasData ? '${snapshot.data}' : '');
    },
  );
  ```

  

- 发送消息

  ```dart
  channel.sink.add('Hello!');
  ```

  

完整demo

```dart
import 'package:flutter/material.dart';
import 'package:web_socket_channel/io.dart';

class WebSocketRoute extends StatefulWidget {
  @override
  _WebSocketRouteState createState() => new _WebSocketRouteState();
}

class _WebSocketRouteState extends State<WebSocketRoute> {
  TextEditingController _controller = new TextEditingController();
  IOWebSocketChannel channel;
  String _text = "";


  @override
  void initState() {
    //创建websocket连接
    channel = new IOWebSocketChannel.connect('ws://echo.websocket.org');
  }

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("WebSocket(内容回显)"),
      ),
      body: new Padding(
        padding: const EdgeInsets.all(20.0),
        child: new Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: <Widget>[
            new Form(
              child: new TextFormField(
                controller: _controller,
                decoration: new InputDecoration(labelText: 'Send a message'),
              ),
            ),
            new StreamBuilder(
              stream: channel.stream,
              builder: (context, snapshot) {
                //网络不通会走到这
                if (snapshot.hasError) {
                  _text = "网络不通...";
                } else if (snapshot.hasData) {
                  _text = "echo: "+snapshot.data;
                }
                return new Padding(
                  padding: const EdgeInsets.symmetric(vertical: 24.0),
                  child: new Text(_text),
                );
              },
            )
          ],
        ),
      ),
      floatingActionButton: new FloatingActionButton(
        onPressed: _sendMessage,
        tooltip: 'Send message',
        child: new Icon(Icons.send),
      ),
    );
  }

  void _sendMessage() {
    if (_controller.text.isNotEmpty) {
      channel.sink.add(_controller.text);
    }
  }

  @override
  void dispose() {
    channel.sink.close();
    super.dispose();
  }
}
```

数据类型：发送的过程中数据以frame形式存在，每一个frame都由opcode字段指定类型，客户端在收到消息时已经知道类型，会自动转换，streamBuilder.snapshot.data如果是文本，类型是string，二进制数据，类型是List<int>,还有其他类型



参考：https://book.flutterchina.club/chapter11/websocket.html