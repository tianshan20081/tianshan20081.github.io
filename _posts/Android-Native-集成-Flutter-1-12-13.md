---
title: Android Native 集成 Flutter 1.12.13
date: 2020-04-22 18:13:20
tags: [Android, Flutter]
categories: [Android, Flutter]
---

### 环境信息

```
 # flutter doctor -v
[✓] Flutter (Channel stable, v1.12.13+hotfix.9, on Mac OS X 10.15.4 19E287, locale zh-Hans-CN)
    • Flutter version 1.12.13+hotfix.9 at /Users/mz/Dev/bin/flutter
    • Framework revision f139b11009 (3 周前), 2020-03-30 13:57:30 -0700
    • Engine revision af51afceb8
    • Dart version 2.7.2
```

### 创建 Android 工程

基本信息:
项目名称 `Flutter_Android`

....略过

**注意:** `com.android.application` 所在 Module 名称 必须为 `app`

### 创建 Flutter Module

基本信息:
项目名称 `flutter_module`

....略过

### Android 工程集成 Flutter Module

#### 修改 Android settings.gradle 文件

```gradle
rootProject.name = 'Flutter_Android'
include ':app'

setBinding(new Binding([gradle: this]))

evaluate(new File(
        settingsDir,
        /* 注意这里需要使用 相对路径 */
        '../flutter_module/.android/include_flutter.groovy'
))
```

**注意:** `../flutter_module/.android/include_flutter.groovy` 需要使用 相对路径。

#### Android 工程添加依赖

`app/build.gradle`

`implementation project(path: ':flutter')`

### Android 调用 Flutter

#### 打开默认工程

```java
public void jumpFlutterDefaultPage(View view) {

  String FLUTTER_ENGINE = "flutter_engine";
  FlutterEngine flutterEngine = new FlutterEngine(this);
  flutterEngine.getDartExecutor().executeDartEntrypoint(DartExecutor.DartEntrypoint.createDefault());

  FlutterEngineCache.getInstance().put(FLUTTER_ENGINE, flutterEngine);
  FlutterActivity.CachedEngineIntentBuilder cachedEngineIntentBuilder = FlutterActivity.withCachedEngine(FLUTTER_ENGINE);

  startActivity(cachedEngineIntentBuilder.build(this));

}
```

#### 打开 Main 页面

```java
public void jumpFlutterMain(View view) {
  startActivity(FlutterActivity.withNewEngine()
          .initialRoute("main")
          .build(this));
}
```

#### 打开我的页面

```java
public void jumpFlutterMine(View view) {

  startActivity(FlutterActivity.withNewEngine()
          .initialRoute("mine")
          .build(this));

}
```

#### 以 View 的方式加载

```java
public void jumpFlutterView(View view) {
    FlutterView flutterView = new FlutterView(this);
    FrameLayout framelayout = findViewById(R.id.framelayout);

    FlutterEngine flutterEngine = new FlutterEngine(this);
    flutterEngine.getDartExecutor().executeDartEntrypoint(
            new DartExecutor.DartEntrypoint(FlutterMain.findAppBundlePath(), "mine")
    );

    flutterView.attachToFlutterEngine(flutterEngine);

    framelayout.addView(flutterView);

}
```

### Flutter 代码

`main.dart`

```dart
import 'dart:ui';

import 'package:flutter/material.dart';
import 'package:fluttermodule/pages/MinePage.dart';

void main() => runApp(MyApp());

void mine() => runApp(MineApp());

class MineApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "Mine App",
      home: MinePage(),
    );
  }
}

class MyApp extends StatelessWidget {
  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        // This is the theme of your application.
        //
        // Try running your application with "flutter run". You'll see the
        // application has a blue toolbar. Then, without quitting the app, try
        // changing the primarySwatch below to Colors.green and then invoke
        // "hot reload" (press "r" in the console where you ran "flutter run",
        // or press Run > Flutter Hot Reload in a Flutter IDE). Notice that the
        // counter didn't reset back to zero; the application is not restarted.
        primarySwatch: Colors.blue,
      ),
      home: _getWidgetByRoute(window.defaultRouteName),
//      routes: <String, WidgetBuilder>{
//        "main": (context) => MyHomePage(),
//        "mine": (context) => MinePage(),
//      },
//      onUnknownRoute: (RouteSettings settings) {
//        return new PageRouteBuilder(pageBuilder: (BuildContext context, _, __) {
//          return MyHomePage(title: "Home Page");
//        });
//      },
    );
  }

  Widget _getWidgetByRoute(String defaultRouteName) {
    print("_getWidgetByRoute:" + defaultRouteName);
    if ("/" == defaultRouteName || "main" == defaultRouteName) {
      return MyHomePage(title: "Home page");
    } else if ("mine" == defaultRouteName) {
      return MinePage();
    }

    return Center(
      child: Text("Default Page"),
    );
  }
}
```

`MinePage.dart`

```dart
import 'package:flutter/material.dart';

class MinePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text("Mine Page"),
    );
  }
}
```
