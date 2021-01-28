---
title: 融云iOS无法接受语音视频消息
date: 2021-01-27 09:03:11
categories: 
- flutter
tags:
---

安卓（李某测试）拨打 苹果（李朴2），进入对话界面，

弹出键盘，弹出报错,在chat_room.dart文件中

```dart
[VERBOSE-2:ui_dart_state.cc(177)] Unhandled Exception: 'package:flutter/src/widgets/scroll_controller.dart': Failed assertion: line 112 pos 12: '_positions.isNotEmpty': ScrollController not attached to any scroll views.
#0      _AssertionError._doThrowNew (dart:core-patch/errors_patch.dart:46:39)
#1      _AssertionError._throwNew (dart:core-patch/errors_patch.dart:36:5)
#2      ScrollController.position (package:flutter/src/widgets/scroll_controller.dart:112:12)
#3      _ChatRoomState.didChangeMetrics (package:polars_app/pages/chat/chat_room.dart:708:27)
#4      WidgetsBinding.handleMetricsChanged (package:flutter/src/widgets/binding.dart:571:16)
#5      _rootRun (dart:async/zone.dart:1190:13)
#6      _CustomZone.run (dart:async/zone.dart:1093:19)
#7      _CustomZone.runGuarded (dart:async/zone.dart:997:7)
#8      _invoke (dart:ui/hooks.dart:251:10)
#9      _updateWindowMetrics (dart:ui/hooks.dart:53:3)
```

解决：在访问maxScrollExtent属性前一定要判断_scrollController.hasClients

```dart
if (_scrollController.hasClients) {
  _scrollController.position.maxScrollExtent;
}
```

问题描述：

```dart
//33003	调用接口时传入的参数不正确
[RC-Flutter-IM] iOS error sendMessage 33003
  
[VERBOSE-2:ui_dart_state.cc(177)] Unhandled Exception: NoSuchMethodError: The method '+' was called on null.
Receiver: null
Tried calling: +(":该消息内容为空，可能该消息没有在原生 SDK 中注册")
#0      Object.noSuchMethod (dart:core-patch/object_patch.dart:51:5)
#1      MessageFactory.map2Message (package:rongcloud_im_plugin/src/util/message_factory.dart:120:40)
#2      MessageFactory.string2Message (package:rongcloud_im_plugin/src/util/message_factory.dart:27:12)
#3      RongIMClient.sendMessageWithCallBack (package:rongcloud_im_plugin/src/rong_im_client.dart:187:43)
<asynchronous suspension>
#4      RongIMClient.sendMessageCarriesPush (package:rongcloud_im_plugin/src/rong_im_client.dart:116:12)
#5      RongIMClient.sendMessage (package:rongcloud_im_plugin/src/rong_im_client.dart:92:12)
#6      _ChatRoomState._sendMessage (package:polars_app/pages/chat/chat_room.dart:2765:32)
#7      _ChatRoomState._sendMessageClick (package:polars_app/pages/chat/chat_room.dart:2144:9)
#8      _ChatRoomState._buildTextComposer.<anonymous closure>.<anonymous closure> (package:polars_app/pages/chat/chat_room.dart:2097:29)
#9      _InkResponseState._handleTap (package:flutter/src/material/ink_well.dart:993:19)
#10     _InkResponseState.build.<anonymous closure> (package:flutter/src/material/ink_well.dart:1111:38)
#11     GestureRecognizer.invokeCallback (package:flutter/src/gestures/recognizer.dart:183:24)
#12     TapGestureRecognizer.handleTapUp (package:flutter/src/gestures/tap.dart:598:11)
#13     BaseTapGestureRecognizer._checkUp (package:flutter/src/gestures/tap.dart:287:5)
#14     BaseTapGestureRecognizer.acceptGesture (package:flutter/src/gestures/tap.dart:259:7)
#15     GestureArenaManager.sweep (package:flutter/src/gestures/arena.dart:157:27)
#16     GestureBinding.handleEvent (package:flutter/src/gestures/binding.dart:362:20)
#17     GestureBinding.dispatchEvent (package:flutter/src/gestures/binding.dart:338:22)
#18     RendererBinding.dispatchEvent (package:flutter/src/rendering/binding.dart:267:11)
#19     GestureBinding._handlePointerEvent (package:flutter/src/gestures/binding.dart:295:7)
#20     GestureBinding._flushPointerEventQueue (package:flutter/src/gestures/binding.dart:240:7)
#21     GestureBinding._handlePointerDataPacket (package:flutter/src/gestures/binding.dart:213:7)
#22     _rootRunUnary (dart:async/zone.dart:1206:13)
#23     _CustomZone.runUnary (dart:async/zone.dart:1100:19)
#24     _CustomZone.runUnaryGuarded (dart:async/zone.dart:1005:7)
#25     _invoke1 (dart:ui/hooks.dart:265:10)
#26     _dispatchPointerDataPacket (dart:ui/hooks.dart:174:5)
```

分析：

```dart
//走到这串代码
msg = await RongIMClient.send
//launch和login调用登录代码
  RyManager.instance.connect();
//方法内部调用  获取到的token为空
RongIMClient.connect(token)
```

无法连接融云，暂停；

继续调试

李朴2  userID：1174605640773193730  

李某测试 userID：1107918162780569602



李某测试 (userID：1107918162780569602)  android

打给 

李朴2 (userID：1174605640773193730)  iOS,锁屏超过一分钟

at 11:56

14：00 等待融云官方回复

app_helper-------->go web page ------->web view

