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

  效果：