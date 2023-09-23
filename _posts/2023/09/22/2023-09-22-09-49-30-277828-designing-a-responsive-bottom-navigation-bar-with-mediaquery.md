---
layout: post
title: "Designing a responsive bottom navigation bar with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [flutter, responsivedesign]
comments: true
share: true
---

In this blog post, we will explore how to design a responsive bottom navigation bar using the `MediaQuery` class in Flutter. The `MediaQuery` class allows us to retrieve the size and orientation of the screen, which helps us adjust the layout of our app based on different screen sizes or orientations.

## Why Responsive Bottom Navigation Bar?

A responsive bottom navigation bar ensures that the navigation bar adapts to different screen sizes, making it easier for users to navigate through the app on various devices. By using `MediaQuery`, we can dynamically alter the layout of the navigation bar based on the available screen width, ensuring a seamless user experience.

## Implementing a Responsive Bottom Navigation Bar

To begin, let's start by creating a new Flutter project and setting up the basic structure of our app. 
In the pubspec.yaml file, add the following dependency:

```dart
dependencies:
  flutter:
    sdk: flutter
  flutter_screenutil: ^4.0.2
```

Next, import the necessary packages for `MediaQuery` and `flutter_screenutil` by adding the following lines of code to the top of your `main.dart` file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';
```

Now, let's define a stateful widget called `BottomNavBar`:

```dart
class BottomNavBar extends StatefulWidget {
  @override
  _BottomNavBarState createState() => _BottomNavBarState();
}

class _BottomNavBarState extends State<BottomNavBar> {
  int _selectedIndex = 0;

  @override
  Widget build(BuildContext context) {
    // TODO: Implement the navigation bar layout based on screen size using MediaQuery

    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Bottom Navigation'),
      ),
      body: Center(
        child: Text('Content of the selected tab'),
      ),
      bottomNavigationBar: BottomNavigationBar(
        items: const <BottomNavigationBarItem>[
          BottomNavigationBarItem(
            icon: Icon(Icons.home),
            label: 'Home',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.business),
            label: 'Business',
          ),
          BottomNavigationBarItem(
            icon: Icon(Icons.school),
            label: 'School',
          ),
        ],
        currentIndex: _selectedIndex,
        onTap: (index) {
          setState(() {
            _selectedIndex = index;
          });
        },
      ),
    );
  }
}
```

Now, it's time to implement the responsive layout using `MediaQuery`. We can use the `MediaQuery.of(context).size.width` to retrieve the screen width and determine the number of navigation bar items to display. 

Update the `build` method of the `_BottomNavBarState` class with the following code:

```dart
@override
  Widget build(BuildContext context) {
    double screenWidth = MediaQuery.of(context).size.width;
    int maxNavItems = 3; // Set the maximum number of navigation bar items
    
    if (screenWidth <= 600) {
      maxNavItems = 2; // Adjust the number of navigation bar items for smaller screens
    }
    
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Bottom Navigation'),
      ),
      body: Center(
        child: Text('Content of the selected tab'),
      ),
      bottomNavigationBar: BottomNavigationBar(
        items: const <BottomNavigationBarItem>[
          // Add the necessary number of navigation items based on maxNavItems
          if (maxNavItems >= 1)
            BottomNavigationBarItem(
              icon: Icon(Icons.home),
              label: 'Home',
            ),
          if (maxNavItems >= 2)
            BottomNavigationBarItem(
              icon: Icon(Icons.business),
              label: 'Business',
            ),
          if (maxNavItems >= 3)
            BottomNavigationBarItem(
              icon: Icon(Icons.school),
              label: 'School',
            ),
        ],
        currentIndex: _selectedIndex,
        onTap: (index) {
          setState(() {
            _selectedIndex = index;
          });
        },
      ),
    );
  }
```

This implementation dynamically adjusts the number of navigation bar items based on the screen width, with a maximum of 3 items. For screens with a width of 600 or less, it displays a maximum of 2 items.

## Conclusion

By utilizing the `MediaQuery` class in Flutter, we can easily design responsive bottom navigation bars. This allows our app to adapt to different screen sizes and provide a seamless navigation experience for users across various devices. Consider using `MediaQuery` along with other responsive design techniques to enhance the overall user experience in your Flutter apps.

```#flutter #responsivedesign```