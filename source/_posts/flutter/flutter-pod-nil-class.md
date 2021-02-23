---
title: flutter NoMethodError - undefined method `size' for nil:NilClass错误排查
date: 2021-2-23 10:50:49
categories: 
- flutter
tags:
---

错误描述: pod install时发生错误

```shell
### Error

​```
NoMethodError - undefined method `size' for nil:NilClass
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho/macho_file.rb:455:in `populate_mach_header'
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho/macho_file.rb:233:in `populate_fields'
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho/macho_file.rb:55:in `initialize_from_bin'
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho/macho_file.rb:33:in `new_from_bin'
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho/fat_file.rb:365:in `block in populate_machos'
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho/fat_file.rb:364:in `each'
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho/fat_file.rb:364:in `populate_machos'
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho/fat_file.rb:156:in `populate_fields'
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho/fat_file.rb:95:in `initialize'
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho.rb:31:in `new'
/Library/Ruby/Gems/2.6.0/gems/ruby-macho-1.4.0/lib/macho.rb:31:in `open'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/xcode/linkage_analyzer.rb:16:in `dynamic_binary?'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/sandbox/file_accessor.rb:171:in `block in vendored_dynamic_frameworks'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/sandbox/file_accessor.rb:170:in `select'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/sandbox/file_accessor.rb:170:in `vendored_dynamic_frameworks'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/sandbox/file_accessor.rb:179:in `vendored_static_frameworks'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/sandbox/file_accessor.rb:292:in `vendored_static_artifacts'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/installer/xcode/target_validator.rb:82:in `each'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/installer/xcode/target_validator.rb:82:in `flat_map'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/installer/xcode/target_validator.rb:82:in `block (2 levels) in verify_no_static_framework_transitive_dependencies'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/installer/xcode/target_validator.rb:74:in `each_key'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/installer/xcode/target_validator.rb:74:in `block in verify_no_static_framework_transitive_dependencies'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/installer/xcode/target_validator.rb:73:in `each'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/installer/xcode/target_validator.rb:73:in `verify_no_static_framework_transitive_dependencies'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/installer/xcode/target_validator.rb:38:in `validate!'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/installer.rb:595:in `validate_targets'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/installer.rb:162:in `install!'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/command/install.rb:52:in `run'
/Library/Ruby/Gems/2.6.0/gems/claide-1.0.3/lib/claide/command.rb:334:in `run'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/lib/cocoapods/command.rb:52:in `run'
/Library/Ruby/Gems/2.6.0/gems/cocoapods-1.10.0/bin/pod:55:in `<top (required)>'
/usr/local/bin/pod:23:in `load'
/usr/local/bin/pod:23:in `<main>'
​```

――― TEMPLATE END ――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――――

[!] Oh no, an error occurred.

Search for existing GitHub issues similar to yours:
https://github.com/CocoaPods/CocoaPods/search?q=undefined+method+%60size%27+for+nil%3ANilClass&type=Issues

If none exists, create a ticket, with the template displayed above, on:
https://github.com/CocoaPods/CocoaPods/issues/new

Be sure to first read the contributing guide for details on how to properly submit a ticket:
https://github.com/CocoaPods/CocoaPods/blob/master/CONTRIBUTING.md

Don't forget to anonymize any private data!

Looking for related issues on cocoapods/cocoapods...
 -  NoMethodError - undefined method `size' for nil:NilClass
   https://github.com/CocoaPods/CocoaPods/issues/10426 [closed] [3 comments]
   a week ago

 - NoMethodError - undefined method `size' for nil:NilClass
   https://github.com/CocoaPods/CocoaPods/issues/10273 [closed] [3 comments]
   7 weeks ago

 - NoMethodError - undefined method `size' for nil:NilClass
   https://github.com/CocoaPods/CocoaPods/issues/8377 [closed] [24 comments]
   a week ago

and 8 more at:
https://github.com/cocoapods/cocoapods/search?q=undefined%20method%20%60size%27%20for%20nil&type=Issues&utf8=✓
```

解决办法：在flutter目录运行以下命令

```shell
flutter clean
rm -Rf ios/Pods
rm -Rf ios/.symlinks
rm -Rf ios/Flutter/Flutter.framework
rm -Rf ios/Flutter/Flutter.podspec
```

参考：https://github.com/CocoaPods/CocoaPods/issues/8377