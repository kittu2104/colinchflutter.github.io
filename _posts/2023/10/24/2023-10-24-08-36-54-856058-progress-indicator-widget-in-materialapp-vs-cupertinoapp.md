---
layout: post
title: "Progress indicator widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [progressindicator]
comments: true
share: true
---

When developing a mobile application, it's important to provide users with feedback on long-running tasks. One common way to achieve this is by using a progress indicator widget. In Flutter, you can choose between two main themes: MaterialApp and CupertinoApp. In this blog post, we will explore how to implement a progress indicator widget in both MaterialApp and CupertinoApp.

## 1. MaterialApp

MaterialApp is the default theme for Flutter applications and provides a modern and visually appealing UI. To add a progress indicator widget to your MaterialApp, follow these steps:

### Step 1: Import the necessary packages

```dart
import 'package:flutter/material.dart';
```

### Step 2: Create a StatefulWidget

```dart
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  bool isLoading = false;
  
  // Other code...
}
```

### Step 3: Implement the progress indicator

```dart
class _MyHomePageState extends State<MyHomePage> {
  bool isLoading = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My App'),
      ),
      body: isLoading
          ? Center(
              child: CircularProgressIndicator(),
            )
          : Center(
              child: RaisedButton(
                child: Text('Start Task'),
                onPressed: () {
                  setState(() {
                    isLoading = true;
                    // Perform your background task here
                  });
                },
              ),
            ),
    );
  }
  // Other code...
}
```

In the above code, we use a `bool` variable `isLoading` to control the visibility of the progress indicator. When the "Start Task" button is pressed, we set `isLoading` to true, which then displays the CircularProgressIndicator. Once the background task is complete, you can set `isLoading` back to false.

## 2. CupertinoApp

CupertinoApp provides an iOS-style theme for your Flutter application. To add a progress indicator widget to your CupertinoApp, follow these steps:

### Step 1: Import the necessary packages

```dart
import 'package:flutter/cupertino.dart';
```

### Step 2: Create a StatefulWidget

```dart
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  bool isLoading = false;
  
  // Other code...
}
```

### Step 3: Implement the progress indicator

```dart
class _MyHomePageState extends State<MyHomePage> {
  bool isLoading = false;

  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('My App'),
      ),
      child: Center(
        child: isLoading
            ? CupertinoActivityIndicator()
            : CupertinoButton(
                child: Text('Start Task'),
                onPressed: () {
                  setState(() {
                    isLoading = true;
                    // Perform your background task here
                  });
                },
              ),
      ),
    );
  }
  // Other code...
}
```

Similar to MaterialApp, we use a `bool` variable `isLoading` to control the visibility of the CupertinoActivityIndicator. When the "Start Task" button is pressed, we set `isLoading` to true, which then shows the activity indicator. Once the background task is complete, you can set `isLoading` back to false.

## Conclusion

MaterialApp and CupertinoApp both provide a convenient way to implement a progress indicator widget in your Flutter application. Choose the theme that best aligns with your target platform's UI guidelines and give your users a seamless experience while indicating progress in your app.

Remember, progress indicators are essential in long-running tasks to keep users informed, so make sure to include them whenever appropriate.

### References
- Flutter Official Documentation: [https://flutter.dev/docs](https://flutter.dev/docs)
- Flutter Cupertino Widgets: [https://pub.dev/packages/cupertino_widgets](https://pub.dev/packages/cupertino_widgets)

#flutter #progressindicator