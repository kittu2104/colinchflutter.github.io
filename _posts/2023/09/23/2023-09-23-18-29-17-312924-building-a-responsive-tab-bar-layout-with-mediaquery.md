---
layout: post
title: "Building a responsive tab bar layout with `MediaQuery`"
description: " "
date: 2023-09-23
tags: []
comments: true
share: true
---

In modern web development, creating responsive user interfaces is a crucial aspect. One common UI pattern is a tab bar, which allows users to easily switch between different sections of an application. In this tutorial, we will explore how to build a responsive tab bar layout using the `MediaQuery` class in Flutter.

### Prerequisites

To follow along with this tutorial, you should have Flutter installed on your machine. You can download Flutter from the official Flutter website and then set up your development environment.

### Getting Started

Let's start by creating a new Flutter project. Open your terminal or command prompt and run the following command:

```
flutter create responsive_tab_bar_layout
```

Once the project is created, navigate to the project directory:

```
cd responsive_tab_bar_layout
```

### Creating the Tab Bar Layout

In Flutter, the `MediaQuery` class allows us to access the current device's screen size and orientation. We can leverage this class to create a responsive tab bar layout that adapts to different screen sizes.

To begin, open the `lib/main.dart` file in your project directory. Replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(TabBarLayoutApp());
}

class TabBarLayoutApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Tab Bar Layout',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TabBarLayout(),
    );
  }
}

class TabBarLayout extends StatefulWidget {
  @override
  _TabBarLayoutState createState() => _TabBarLayoutState();
}

class _TabBarLayoutState extends State<TabBarLayout> {
  int _currentIndex = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Tab Bar Layout'),
      ),
      body: Column(
        children: [
          Expanded(
            child: IndexedStack(
              index: _currentIndex,
              children: [
                Container(
                  color: Colors.red,
                ),
                Container(
                  color: Colors.green,
                ),
                Container(
                  color: Colors.blue,
                ),
              ],
            ),
          ),
          _buildTabBar(),
        ],
      ),
    );
  }

  Widget _buildTabBar() {
    return MediaQuery.of(context).size.width >= 600
        ? _buildDesktopTabBar()
        : _buildMobileTabBar();
  }

  Widget _buildDesktopTabBar() {
    return Container(
      color: Colors.grey.shade200,
      padding: EdgeInsets.symmetric(vertical: 16.0),
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children: [
          _buildTabItem('Tab 1', 0),
          _buildTabItem('Tab 2', 1),
          _buildTabItem('Tab 3', 2),
        ],
      ),
    );
  }

  Widget _buildMobileTabBar() {
    return BottomNavigationBar(
      currentIndex: _currentIndex,
      onTap: (index) {
        setState(() {
          _currentIndex = index;
        });
      },
      items: [
        BottomNavigationBarItem(
          icon: Icon(Icons.tab),
          label: 'Tab 1',
        ),
        BottomNavigationBarItem(
          icon: Icon(Icons.tab),
          label: 'Tab 2',
        ),
        BottomNavigationBarItem(
          icon: Icon(Icons.tab),
          label: 'Tab 3',
        ),
      ],
    );
  }

  Widget _buildTabItem(String title, int index) {
    return GestureDetector(
      onTap: () {
        setState(() {
          _currentIndex = index;
        });
      },
      child: Text(
        title,
        style: TextStyle(
          fontSize: 16.0,
          fontWeight: FontWeight.bold,
          color: _currentIndex == index ? Colors.blue : Colors.grey,
        ),
      ),
    );
  }
}
```

In this example, we define a `TabBarLayoutApp` widget as the entry point of our Flutter application. The `TabBarLayout` widget represents our tab bar layout, and it is a stateful widget that manages the current index of the active tab.

Inside the `Scaffold` of the `TabBarLayout` widget, we create a column layout. The first child is an `Expanded` widget that contains an `IndexedStack`. This allows us to switch between different content views based on the selected tab.

Inside the `Column`, we also call the `_buildTabBar()` method to determine which tab bar implementation to display based on the screen size. For screens wider than 600 pixels, we render a desktop-style tab bar with horizontal tabs. For narrower screens, we use a `BottomNavigationBar` with vertical tabs.

The `_buildDesktopTabBar()` method defines a container with a row layout and evenly spaced tabs. The `_buildMobileTabBar()` method creates a `BottomNavigationBar` with vertical tabs that change the active tab on tap.

Finally, the `_buildTabItem()` method creates a widget for each individual tab, displaying the tab's title and updating the current index when tapped.

### Testing the Tab Bar Layout

To test the responsive tab bar layout, run the following command in your terminal or command prompt:

```
flutter run
```

This will launch the Flutter app on the simulator or connected device. You can then interact with the tab bar layout and observe how it adapts to different screen sizes.

### Conclusion

In this tutorial, we have explored how to build a responsive tab bar layout using the `MediaQuery` class in Flutter. By leveraging the device's screen size and orientation, we can create flexible user interfaces that provide an optimal experience across various devices.