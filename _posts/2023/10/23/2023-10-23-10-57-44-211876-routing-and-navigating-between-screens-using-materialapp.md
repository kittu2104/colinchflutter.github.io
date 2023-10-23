---
layout: post
title: "Routing and navigating between screens using MaterialApp."
description: " "
date: 2023-10-23
tags: [mobile]
comments: true
share: true
---

In any mobile or web application, proper navigation between screens is a crucial aspect of providing a seamless user experience. In Flutter, the "MaterialApp" widget plays a key role in handling app navigation by managing routes and transitions between different screens.

To implement routing and screen navigation using the MaterialApp widget, follow the steps below:

## 1. Add the MaterialApp widget to the main.dart file

In the main.dart file, wrap your app's widget with the MaterialApp widget as follows:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      // Define the initial route
      initialRoute: '/',
      // Define the routes
      routes: {
        '/': (context) => HomePage(),
        '/second': (context) => SecondScreen(),
        '/third': (context) => ThirdScreen(),
      },
    );
  }
}
```

In the above code snippet, we define the initial route as `'/'` and define other named routes (e.g., `'/second'` and `'/third'`) along with their corresponding screen widgets (`HomePage()`, `SecondScreen()`, and `ThirdScreen()`).

## 2. Navigating to a different screen

To navigate to a different screen when a button or any other user interaction occurs, use the `Navigator.pushNamed()` method as shown below:

```dart
...
RaisedButton(
  onPressed: () {
    Navigator.pushNamed(context, '/second');
  },
  child: Text('Go to Second Screen'),
),
...
```

The `Navigator.pushNamed()` method pushes the screen with the specified route name onto the navigation stack, causing the app to navigate to the desired screen.

## 3. Passing data between screens

To pass data between screens, you can pass arguments along with the route using the `Navigator.pushNamed()` method. For example:

```dart
...
RaisedButton(
  onPressed: () {
    Navigator.pushNamed(
      context,
      '/third',
      arguments: {'name': 'John', 'age': 25},
    );
  },
  child: Text('Go to Third Screen'),
),
...
```

In the above code snippet, we pass a map of arguments containing the name and age to the `/third` route.

## 4. Accessing passed data in the destination screen

To access the passed data in the destination screen, use the `ModalRoute.of(context).settings.arguments` property. For instance:

```dart
...
class ThirdScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final Map<String, dynamic> arguments =
        ModalRoute.of(context).settings.arguments;
    
    final String name = arguments['name'];
    final int age = arguments['age'];

    return Scaffold(
      appBar: AppBar(
        title: Text('Third Screen'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Name: $name'),
            Text('Age: $age'),
          ],
        ),
      ),
    );
  }
}
...
```

In the above code snippet, we retrieve the passed arguments using `ModalRoute.of(context).settings.arguments` and then access the name and age values in the `ThirdScreen` widget.

With the MaterialApp widget and the Navigator class, you can easily implement routing and navigate between screens in your Flutter app. By following the steps above, you'll have a well-structured navigation system that enhances user experience and helps users navigate through your app seamlessly.

# Conclusion

In this article, we explored how to implement routing and navigation between screens using the MaterialApp widget in Flutter. By leveraging the power of the MaterialApp widget and the Navigator class, you can build robust and user-friendly applications that provide a smooth and intuitive navigation experience for your users.

# References
- Official Flutter Documentation: [https://flutter.dev/docs/development/ui/navigation](https://flutter.dev/docs/development/ui/navigation)
- Flutter Navigation and Routing Guide: [https://flutter.dev/docs/cookbook/navigation/navigation-basics](https://flutter.dev/docs/cookbook/navigation/navigation-basics)

**#flutter #mobile-apps**