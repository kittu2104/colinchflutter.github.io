---
layout: post
title: "Setting up an initial route in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

When building a Flutter app, one of the first steps is to set up the initial route. The initial route determines the first screen that users will see when they open the app.

In Flutter, the `MaterialApp` widget is commonly used as the root widget of the app. It provides several configuration options, including setting up the initial route.

To set up the initial route in `MaterialApp`, you can use the `initialRoute` property. Let's take a look at an example:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      initialRoute: '/',
      routes: {
        '/': (context) => HomeScreen(),
        '/second': (context) => SecondScreen(),
      },
      // other configurations
    );
  }
}

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Center(
        child: Text('Welcome to the Home screen!'),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Second Screen'),
      ),
      body: Center(
        child: Text('This is the second screen.'),
      ),
    );
  }
}
```

In this example, we define two routes: `/` for the `HomeScreen` and `/second` for the `SecondScreen`. The `initialRoute` property is set to `'/'`, so when the app starts, it will display the `HomeScreen`.

To navigate to the `SecondScreen`, you can use the `Navigator.pushNamed()` method and provide the route name:

```dart
Navigator.pushNamed(context, '/second');
```

By setting up the initial route in the `MaterialApp`, you can easily control the first screen that your users see when they open your app. This allows you to create a consistent user experience and navigate between different screens effortlessly.

# Conclusion

Setting up an initial route in `MaterialApp` is a crucial step in building a Flutter app. By using the `initialRoute` property, you can define the first screen that users will see when they open the app.