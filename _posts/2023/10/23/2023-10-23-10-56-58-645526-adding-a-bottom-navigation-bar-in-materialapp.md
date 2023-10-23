---
layout: post
title: "Adding a bottom navigation bar in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

The bottom navigation bar is a common UI element used in mobile applications to provide easy access to different sections or functionalities of the app. In this tutorial, we will learn how to add a bottom navigation bar in a MaterialApp using the Flutter framework.

## Table of Contents
* [Prerequisites](#prerequisites)
* [Setting Up the Project](#setting-up-the-project)
* [Adding Bottom Navigation Bar](#adding-bottom-navigation-bar)
* [Handling Navigation](#handling-navigation)
* [Customizing the Bottom Navigation Bar](#customizing-the-bottom-navigation-bar)
* [Conclusion](#conclusion)

## Prerequisites

Make sure you have Flutter installed on your development environment. You can download and install Flutter from the official Flutter website: [flutter.dev](https://flutter.dev).

## Setting Up the Project

To create a new Flutter project, open a terminal or command prompt and run the following command:

```dart
flutter create bottom_navigation_app
```

This command will create a new Flutter project named `bottom_navigation_app`.

## Adding Bottom Navigation Bar

Open the `lib/main.dart` file in your project and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(BottomNavigationApp());
}

class BottomNavigationApp extends StatefulWidget {
  @override
  _BottomNavigationAppState createState() => _BottomNavigationAppState();
}

class _BottomNavigationAppState extends State<BottomNavigationApp> {
  int _selectedIndex = 0;

  final List<Widget> _widgetOptions = [
    HomePage(),
    SearchPage(),
    ProfilePage(),
  ];

  void _onItemTapped(int index) {
    setState(() {
      _selectedIndex = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Bottom Navigation App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Bottom Navigation App'),
        ),
        body: _widgetOptions.elementAt(_selectedIndex),
        bottomNavigationBar: BottomNavigationBar(
          currentIndex: _selectedIndex,
          onTap: _onItemTapped,
          items: [
            BottomNavigationBarItem(
              icon: Icon(Icons.home),
              label: 'Home',
            ),
            BottomNavigationBarItem(
              icon: Icon(Icons.search),
              label: 'Search',
            ),
            BottomNavigationBarItem(
              icon: Icon(Icons.person),
              label: 'Profile',
            ),
          ],
        ),
      ),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text('Home Page'),
    );
  }
}

class SearchPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text('Search Page'),
    );
  }
}

class ProfilePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Center(
      child: Text('Profile Page'),
    );
  }
}
```

In the code above, we define a `BottomNavigationApp` widget which extends a `StatefulWidget`. Inside the `BottomNavigationApp`, we have a private `_selectedIndex` variable that keeps track of the selected item index in the bottom navigation bar.

We also have a list of widgets `_widgetOptions` that represents the different pages accessed via the bottom navigation bar.

The `BottomNavigationApp` widget contains a `bottomNavigationBar` property which is a `BottomNavigationBar` widget. The `BottomNavigationBar` is configured with three items, each representing a corresponding page in the `_widgetOptions` list.

The `onTap` property of the `BottomNavigationBar` is set to `_onItemTapped` function which updates the `_selectedIndex` value when a different item is tapped.

The `body` property of the `Scaffold` is set to `_widgetOptions.elementAt(_selectedIndex)` which displays the selected page from the `_widgetOptions` list.

Finally, we create three separate `StatelessWidget` classes for the home, search, and profile pages, each displaying a simple centered text.

## Handling Navigation

To handle navigation between the different pages within the bottom navigation bar, we use the `_selectedIndex` value and update it accordingly in the `_onItemTapped` function.

You can add custom logic inside the `_onItemTapped` function to handle any additional actions or navigation requirements specific to your app.

## Customizing the Bottom Navigation Bar

You can customize the appearance of the bottom navigation bar by changing the colors, icons, or labels used in the `BottomNavigationBarItem` widgets.

You can also add more items to the `BottomNavigationBar` by extending the `_widgetOptions` list and adding corresponding pages.

## Conclusion

In this tutorial, we have learned how to add a bottom navigation bar in a MaterialApp using Flutter. We also explored how to handle navigation and customize the appearance of the bottom navigation bar.

Feel free to experiment and add more functionality to your bottom navigation bar based on the specific requirements of your app.

# References
* Flutter Documentation: [https://flutter.dev/docs](https://flutter.dev/docs)
* BottomNavigationBar Class: [https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html](https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html)