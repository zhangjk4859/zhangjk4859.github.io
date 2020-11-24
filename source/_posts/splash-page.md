---
title: flutter启动页
date: 2020-11-24 14:09:04
tags:
---

在main.dart文件的materialAPP.home属性返回一个UI，这个UI就是启动页，启动页的scanffold的body，返回一张图片

- in main.dart

```
return MaterialApp(
          home: SplashPage(),
        );
```

- in SplashPage

  ```
  @override
    Widget build(BuildContext context) {
      return Scaffold(
        body: Container(
          child: Image.asset(
            'assets/images/launch_image.png',
            fit: BoxFit.fill,
            width: double.infinity,
            height: double.infinity,
          ),
        ),
      );
    }
  ```

  

