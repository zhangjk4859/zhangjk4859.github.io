---
title: flutter安卓开启第二引擎跑网页
date: 2021-7-2 11:43:01
categories: 
- flutter
tags:
---

​    在纯flutter应用里打开网页，目前流行两个插件:

-  [flutter_webview_plugin](https://pub.flutter-io.cn/packages/flutter_webview_plugin) (以下简称**三方web**)

  - 特点

    >1.实测中滑动相对流畅
    >
    >2.bug较少
    >
    >3.不在flutter的widget tree中，视图在app最顶层，通过channel通知来实现显示和隐藏，全局是一个单例
    >
    >4.非官方

- [webview_flutter](https://pub.flutter-io.cn/packages/webview_flutter)(以下简称**官方web**)

  - 特点

    > 1.镶嵌在widget tree中，方便在flutter中控制
    >
    > 2.键盘弹出有部分bug
    >
    > 3.官方支持

由于历史原因和开发成本考虑，继续沿用三方web作为浏览器，遇到一个需求，就是需要打开网页的时候秒开，实现类似[今日头条的效果](https://blog.csdn.net/zhenghhgz/article/details/112302985)，经过调研和结合flutter特性，最终方案定型为下图

![image](https://github.com/zhangjk4859/zhangjk4859.github.io/blob/zjk/pics/android-flutter-db-engine.png?raw=true)

![image](https://github.com/zhangjk4859/zhangjk4859.github.io/blob/zjk/pics/iOS-flutter-db-engine.png?raw=true)

​    在实现iOS过程中比较顺利，在appdelegate启动的时候加载WebViewController放在后台待命，MainViewController新增一个导航在合适的时候来push WebViewController

```swift
    lazy var webViewEngine:FlutterEngine = {
        let engine = FlutterEngine(name: "webViewEngineName")
        engine.run(withEntrypoint: "webViewMain")
        return engine
    }()
    
    lazy var webViewFlutterVC:FlutterViewController = {
        let webFlutterVC = FlutterViewController(engine: self.webViewEngine, nibName: nil, bundle: nil)
        webFlutterVC.view.backgroundColor = UIColor.white
        return webFlutterVC
    }()

    lazy var registerWebFlutterVC: Void = {
        CopiedPluginRegistrant.register(with: self.webViewFlutterVC)   
        }()


override func application(
    _ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
  ) -> Bool {
    //启动WebViewController
    _ = self.registerWebFlutterVC
  
    return super.application(application, didFinishLaunchingWithOptions: launchOptions)
  }

```

同样的原理框架在实现安卓的时候因为实现原理不同，做了改动：

1. 两个页面均由activity实现，在安卓app启动的时候需要指定一个activity作为单例launcher，把web activity作为launcher先启动，等内部webview预热完成，再启动main activity

manifest文件配置

```html
        <activity
            android:name=".FlutterWebViewActivity"
            android:launchMode="singleInstance"
            android:theme="@style/activityTheme">

            <!--启动先预热第二引擎页面，oncreate里面再切换回app主页-->
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>

            <!--启动的时候加背景图防止黑屏-->
            <meta-data
                android:name="io.flutter.embedding.android.SplashScreenDrawable"
                android:resource="@drawable/launch_background" />


        </activity>

```



2. 在预热web activity过程中，如果不注意两个activity engine注册插件先后顺序和冲突，会出现flutter和原生交互找不到method方法报错，需要按照下面的顺序来

   - 在Application onCreate方法里预热web引擎，automaticallyRegisterPlugins一定要传false

     ```kotlin
     public class MyApp extends FlutterApplication {
         @Override
         public void onCreate() {
             super.onCreate();
     
             //启动预加载一个引擎for 单例 webview 不自动注册插件
             FlutterEngine webEngine = new FlutterEngine(this,null,false);
             FlutterEngineCache.getInstance().put(WebEngine.ENGINE_ID,webEngine);
     
         }
     }
     ```

- - 继承FlutterActivity类，覆写获取engine方法，拿到已经预热好的engine

    ```kotlin
        //加载预热的引擎，在my_app类中创建
        override fun provideFlutterEngine(context: Context): FlutterEngine? {
            //return super.provideFlutterEngine(context)
            return FlutterEngineCache.getInstance().get(WebEngine.ENGINE_ID)
        }
    ```

- - 执行指定的entry point

    ```kotlin
        override fun configureFlutterEngine(flutterEngine: FlutterEngine) {
            runEntrypoint(flutterEngine)
            super.configureFlutterEngine(flutterEngine)
        }
    ```

    

这样，两端就都可以实现H5“秒开”体验。

完。

