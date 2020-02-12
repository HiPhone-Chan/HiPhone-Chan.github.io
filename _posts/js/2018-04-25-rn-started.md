react native初步使用
===================

# 创建工程
react-native init app

# 开发运行
```
react-native run-ios
react-native run-android
```

# 重新加载
```
# 在android 的sdk/platform-tools下
./adb reverse tcp:8081 tcp:8081
or
./adb shell input keyevent 82
```

# 打包
  先执行命令
```
android
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/

ios
react-native bundle --entry-file index.ios.js --platform ios --dev false --bundle-output release_ios/main.jsbundle --assets-dest release_ios/
```
   然后按照各自原生的打包即可