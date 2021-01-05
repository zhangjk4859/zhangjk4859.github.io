---
title: mac android studio flutter 打包 apk
date: 2020-11-16 20:16:07
categories: 
- unix
tags:
---
- Create a keystore

```
keytool -genkey -v -keystore ~/key.jks -keyalg RSA -keysize 2048 -validity 10000 -alias key

```
- <app dir>/android文件夹下生成属性文件关联秘钥 key.properties

```
storePassword=<password from previous step>
keyPassword=<password from previous step>
keyAlias=key
storeFile=<location of the key store file, such as /Users/<user name>/key.jks>

```

- <app dir>/android/app/build.gradle文件里增加load代码

```
def keystoreProperties = new Properties()
   def keystorePropertiesFile = rootProject.file('key.properties')
   if (keystorePropertiesFile.exists()) {
       keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
   }

   android {
         ...
   }
```
- 在buildTypes之前增加签名配置代码

```
signingConfigs {
       release {
           keyAlias keystoreProperties['keyAlias']
           keyPassword keystoreProperties['keyPassword']
           storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
           storePassword keystoreProperties['storePassword']
       }
   }
   buildTypes {
       release {
           signingConfig signingConfigs.release
       }
   }
```

- 运行编译命令

```
flutter build apk
```
- 运行结果

```
Running Gradle task 'assembleRelease'... Done                     143.3s (!)
✓ Built build/app/outputs/flutter-apk/app-release.apk (79.9MB).

```
#### 完。

参考：https://flutter.dev/docs/deployment/android
