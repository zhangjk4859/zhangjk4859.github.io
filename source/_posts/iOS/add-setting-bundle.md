---
title: iOS APP切换网络环境
date: 2021-11-26 11:12:48
categories: 
- iOS
tags:
---

 ### 需求描述：

打一次包，用户可以自由切换开发和生产环境

### 实现原理

每一个app在设置界面可以增加配置选项，存的数据可以通过user default读取，根据存储的数据来甄别切换网络

### 实现步骤

- 新增setting bundle ![image](https://img-blog.csdn.net/20140324110122843?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbm9nb2Rvc3M=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

  ![image](https://img-blog.csdn.net/20140324110154343?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbm9nb2Rvc3M=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

  root.plist source code 如下

  ```json
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
  <plist version="1.0">
  <dict>
  	<key>StringsTable</key>
  	<string>Root</string>
  	<key>PreferenceSpecifiers</key>
  	<array>
  		<dict>
  			<key>Type</key>
  			<string>PSMultiValueSpecifier</string>
  			<key>Title</key>
  			<string>环境</string>
  			<key>Key</key>
  			<string>env_key</string>
  			<key>DefaultValue</key>
  			<string>1</string>
  			<key>Titles</key>
  			<array>
  				<string>DEV</string>
  				<string>TEST</string>
  				<string>PROD</string>
  				<string>SAAS</string>
  			</array>
  			<key>Values</key>
  			<array>
  				<string>1</string>
  				<string>2</string>
  				<string>3</string>
  				<string>4</string>
  			</array>
  		</dict>
  	</array>
  </dict>
  </plist>
  
  ```

  效果：![image](https://github.com/zhangjk4859/zhangjk4859.github.io/blob/zjk/pics/setting-bundle-2.jpg?raw=true)
  
  
  
  ![image](https://github.com/zhangjk4859/zhangjk4859.github.io/blob/zjk/pics/setting-bundle-1.jpg?raw=true)
  
  

- 代码获取值

  ```objective-c
  - (void)registerDefaultsFromSettingsBundle{
      NSString *settingsBundle = [[NSBundle mainBundle] pathForResource:@"Settings" ofType:@"bundle"];
  
      if(!settingsBundle) {
          NSLog(@"Could not find Settings.bundle");
          return;
      }
  
      NSDictionary *settings = [NSDictionary dictionaryWithContentsOfFile:[settingsBundle stringByAppendingPathComponent:@"Root.plist"]];
  
      NSArray *preferences = [settings objectForKey:@"PreferenceSpecifiers"];
  
      NSMutableDictionary *defaultsToRegister = [[NSMutableDictionary alloc] initWithCapacity:[preferences count]];
  
      for(NSDictionary *prefSpecification in preferences) {
          NSString *key = [prefSpecification objectForKey:@"Key"];
  
           if(key) {
              [defaultsToRegister setObject:[prefSpecification objectForKey:@"DefaultValue"] forKey:key];
          }
  
      }
  
      [[NSUserDefaults standardUserDefaults] registerDefaults:defaultsToRegister];
  }
  
  
  -(NSString *)getNetworkOption{
  #if DEBUG
      id obj = [[NSUserDefaults standardUserDefaults] objectForKey:@"env_key"];
      if ([obj isKindOfClass:[NSString class]]) {
          return (NSString *)obj;
      }
      return @"";
  
  #else
      return @"";
  
  #endif
      
  }
  ```





- 设置release状态不包含bundle文件

  Xcode---->Project---->Build Settings---->Build Options---->Exclude Source Files Names---->Release 把文件拖进去



完。

参考：https://blog.csdn.net/nogodoss/article/details/21938771