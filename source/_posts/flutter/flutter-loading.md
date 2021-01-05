---
title: flutter中一个好用的三方库loading
date: 2021-01-05 10:47:15
tags:
---

地址：https://github.com/kokohuang/flutter_easyloading

用法，添加到materialApp的builder属性中

```dart
class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter EasyLoading',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(title: 'Flutter EasyLoading'),
      builder: EasyLoading.init(),
    );
  }
}
```



接下来在任何地方调用

```dart
EasyLoading.show(status: 'loading...');

EasyLoading.showProgress(0.3, status: 'downloading...');

EasyLoading.showSuccess('Great Success!');

EasyLoading.showError('Failed with Error');

EasyLoading.showInfo('Useful Information.');

EasyLoading.showToast('Toast');

EasyLoading.dismiss();
```



示例图片

![image](https://raw.githubusercontent.com/kokohuang/flutter_easyloading/master/images/gif01.gif)