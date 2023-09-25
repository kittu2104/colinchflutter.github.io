---
layout: post
title: "Creating a responsive tab view using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [responsive, tabview]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive tab view using the `MediaQuery` class in Flutter. A tab view allows users to navigate between multiple screens or sections by tapping on tabs.

## Requirements

Before we start, make sure you have the following prerequisites:

- Flutter SDK installed on your machine
- A code editor (such as Visual Studio Code)

## Step 1: Set up the Flutter project

First, let's create a new Flutter project using the terminal or command prompt.

```dart
$ flutter create responsive_tab_view
```

Once the project is created, navigate to the project directory:

```dart
$ cd responsive_tab_view
```

## Step 2: Create the main tab view

Open the `lib/main.dart` file in your code editor, and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(ResponsiveTabViewApp());
}

class ResponsiveTabViewApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Tab View',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: TabViewScreen(),
    );
  }
}

class TabViewScreen extends StatefulWidget {
  @override
  _TabViewScreenState createState() => _TabViewScreenState();
}

class _TabViewScreenState extends State<TabViewScreen> {
  int _currentIndex = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Tab View'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Tab ${_currentIndex + 1}',
              style: TextStyle(
                fontSize: 32,
                fontWeight: FontWeight.bold,
              ),
            ),
          ],
        ),
      ),
      bottomNavigationBar: BottomNavigationBar(
        currentIndex: _currentIndex,
        onTap: (index) {
          setState(() {
            _currentIndex = index;
          });
        },
        items: [
          BottomNavigationBarItem(
            icon: Icon(Icons.home),
            label: 'Tab 1',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.notifications),
            label: 'Tab 2',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.person),
            label: 'Tab 3',
          ),
        ],
      ),
    );
  }
}
```

In this code snippet, we have created a basic Flutter app with a `TabViewScreen` that contains a column with a text widget displaying the current tab index. We have also added a `BottomNavigationBar` to switch between tabs.

## Step 3: Make the tab view responsive

To make the tab view responsive, we will use the `MediaQuery` class to check the screen size and update the layout accordingly.

In the `_TabViewScreenState` class, add the following code snippet inside the `build` method:

```dart
double screenWidth = MediaQuery.of(context).size.width;
if (screenWidth >= 600) {
  // Large screen layout
  return Row(
    children: [
      Expanded(
        flex: 3,
        child: Container(),
      ),
      Expanded(
        flex: 7,
        child: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text(
                'Tab ${_currentIndex + 1}',
                style: TextStyle(
                  fontSize: 32,
                  fontWeight: FontWeight.bold,
                ),
              ),
            ],
          ),
        ),
      ),
    ],
  );
} else {
  // Small screen layout
  return Scaffold(
    appBar: AppBar(
      title: Text('Responsive Tab View'),
    ),
    body: Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Text(
            'Tab ${_currentIndex + 1}',
            style: TextStyle(
              fontSize: 32,
              fontWeight: FontWeight.bold,
            ),
          ),
        ],
      ),
    ),
    bottomNavigationBar: BottomNavigationBar(
      currentIndex: _currentIndex,
     ...
```

In this code snippet, we check the screen width using `MediaQuery.of(context).size.width`. If the width is greater than or equal to 600 (which means it's a large screen), we render a row layout with two expanded containers. Otherwise, we use the default small screen layout similar to the previous code.

## Step 4: Running the app

To run the app, open the terminal or command prompt and execute the following command:

```dart
$ flutter run
```

After the build process is complete, you will see the app running on your selected device or simulator. You can now test the responsive behavior of the tab view by resizing the window or using different devices in the Flutter emulator.

## Conclusion

Congratulations! You have successfully created a responsive tab view using `MediaQuery` in Flutter. With this technique, you can easily adapt your app's layout based on the device's screen size. Feel free to customize the tab view further according to your project requirements.

#flutter #responsive #tabview