---
title: flutter App 优化实操
date: 2021-4-11 17:50:00
categories: 
- flutter
tags:
---

- 抽取widget，尽量成为一个stateless widget

  ```dart
  class MainWidget extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Expanded(
        child: Container(
          color: Colors.grey[700],
          child: Center(
            child: Text(
              'Hello Flutter',
              style: Theme.of(context).textTheme.display1,
            ),
          ),
        ),
      );
    }
  }
  ```

  

- 更新属性值，用传值的方式

  - ChangeNotifier

    ```
    //------ ChangeNotifier class ----//
    class MyColorNotifier extends ChangeNotifier {
      Color myColor = Colors.grey;
      Random _random = new Random();
    
      void changeColor() {
        int randomNumber = _random.nextInt(30);
        myColor = Colors.primaries[randomNumber % Colors.primaries.length];
        notifyListeners();
      }
    }
    //------ State class ----//
    
    class _MyHomePageState extends State<MyHomePage> {
      final _colorNotifier = MyColorNotifier();
    
      void _onPressed() {
        _colorNotifier.changeColor();
      }
    
      @override
      void dispose() {
        _colorNotifier.dispose();
        super.dispose();
      }
    
      @override
      Widget build(BuildContext context) {
        print('building `MyHomePage`');
        return Scaffold(
          floatingActionButton: FloatingActionButton(
            onPressed: _onPressed,
            child: Icon(Icons.colorize),
          ),
          body: Stack(
            children: [
              Positioned.fill(
                child: BackgroundWidget(),
              ),
              Center(
                child: AnimatedBuilder(
                  animation: _colorNotifier,
                  builder: (_, __) => Container(
                    height: 150,
                    width: 150,
                    color: _colorNotifier.myColor,
                  ),
                ),
              ),
            ],
          ),
        );
      }
    }
    ```

    

  - ValueNotifier

    ```dart
    class _MyHomePageState extends State<MyHomePage> {
      final _colorNotifier = ValueNotifier<Color>(Colors.grey);
      Random _random = new Random();
    
      void _onPressed() {
        int randomNumber = _random.nextInt(30);
        _colorNotifier.value =
            Colors.primaries[randomNumber % Colors.primaries.length];
      }
    
      @override
      void dispose() {
        _colorNotifier.dispose();
        super.dispose();
      }
    
      @override
      Widget build(BuildContext context) {
        print('building `MyHomePage`');
        return Scaffold(
          floatingActionButton: FloatingActionButton(
            onPressed: _onPressed,
            child: Icon(Icons.colorize),
          ),
          body: Stack(
            children: [
              Positioned.fill(
                child: BackgroundWidget(),
              ),
              Center(
                child: ValueListenableBuilder(
                  valueListenable: _colorNotifier,
                  builder: (_, value, __) => Container(
                    height: 150,
                    width: 150,
                    color: value,
                  ),
                ),
              ),
            ],
          ),
        );
      }
    }
    ```

- 使用const修饰stateless widget，set state不会重复刷新

  ```dart
  class BackgroundWidget extends StatelessWidget {
    const BackgroundWidget();
  
    @override
    Widget build(BuildContext context) {
      print('building `BackgroundWidget`');
      return Image.network(
        'https://cdn.pixabay.com/photo/2017/08/30/01/05/milky-way-2695569_960_720.jpg',
        fit: BoxFit.cover,
      );
    }
  }
  ```

  

- 生成列表的时候使用itemExtent属性告诉系统item高度，更高效的滑动

  ```dart
  class MyHomePage extends StatelessWidget {
    final widgets = List.generate(
      10000,
      (index) => Container(
        color: Colors.primaries[index % Colors.primaries.length],
        child: ListTile(
          title: Text('Index: $index'),
        ),
      ),
    );
  
    final _scrollController = ScrollController();
  
    void _onPressed() async {
      _scrollController.jumpTo(
        _scrollController.position.maxScrollExtent,
      );
    }
  
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        floatingActionButton: FloatingActionButton(
          onPressed: _onPressed,
          splashColor: Colors.red,
          child: Icon(Icons.slow_motion_video),
        ),
        body: ListView(
          controller: _scrollController,
          children: widgets,
          itemExtent: 200,
        ),
      );
    }
  }
  ```

  

- 需要动画的子控件设置给AnimatedBuilder的child，避免重复绘制

  ```dart
  @override
    Widget build(BuildContext context) {
      return Scaffold(
        floatingActionButton: FloatingActionButton(
          onPressed: _onPressed,
          splashColor: Colors.red,
          child: Icon(Icons.slow_motion_video),
        ),
        body: AnimatedBuilder(
          animation: _controller,
          child: CounterWidget(
            counter: counter,
          ),
          builder: (_, child) => Transform(
            alignment: Alignment.center,
            transform: Matrix4.identity()
              ..setEntry(3, 2, 0.001)
              ..rotateY(360 * _controller.value * (pi / 180.0)),
            child: child,
          ),
        ),
      );
    }
  ```

  

- 合理使用opacity属性，减少调用setlayer方法，触发离屏渲染

  - 使用fadeTransition

    ```dart
    class _MyHomePageState extends State<MyHomePage>
        with SingleTickerProviderStateMixin {
      AnimationController _controller;
      int counter = 0;
    
      void _onPressed() {
        setState(() {
          counter++;
        });
        _controller.forward(from: 0.0);
      }
    
      @override
      void initState() {
        _controller = AnimationController(
            vsync: this, duration: const Duration(milliseconds: 600));
        _controller.addStatusListener((status) {
          if (status == AnimationStatus.completed) {
            _controller.reverse();
          }
        });
        super.initState();
      }
    
      @override
      void dispose() {
        _controller.dispose();
        super.dispose();
      }
    
      @override
      Widget build(BuildContext context) {
        return Scaffold(
          floatingActionButton: FloatingActionButton(
            onPressed: _onPressed,
            splashColor: Colors.red,
            child: Icon(Icons.slow_motion_video),
          ),
          body: FadeTransition(
            opacity: Tween(begin: 1.0, end: 0.0).animate(_controller),
            child: CounterWidget(
              counter: counter,
            ),
          ),
        );
      }
    }
    ```

    

  - 使用animatedOpacity

  ```dart
  const duration = const Duration(milliseconds: 600);
  
  class _MyHomePageState extends State<MyHomePage> {
    int counter = 0;
    double opacity = 1.0;
  
    void _onPressed() async {
      counter++;
      setState(() {
        opacity = 0.0;
      });
      await Future.delayed(duration);
      setState(() {
        opacity = 1.0;
      });
    }
  
    @override
    Widget build(BuildContext context) {
      return Scaffold(
        floatingActionButton: FloatingActionButton(
          onPressed: _onPressed,
          splashColor: Colors.red,
          child: Icon(Icons.slow_motion_video),
        ),
        body: AnimatedOpacity(
          opacity: opacity,
          duration: duration,
          child: CounterWidget(
            counter: counter,
          ),
        ),
      );
    }
  }
  ```

  

完。

sources:

- https://blog.codemagic.io/how-to-improve-the-performance-of-your-flutter-app./
- https://pluscool.cn/2021/03/31/flutter/flutter-app-optimize/

