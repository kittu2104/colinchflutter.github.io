---
layout: post
title: "Designing a responsive navigation drawer using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [responsivedrawer]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive navigation drawer using `MediaQuery` in Flutter. A navigation drawer is a common UI pattern that allows users to access various app screens or functionalities by sliding the drawer from the left edge of the screen. With the help of `MediaQuery`, we can make the navigation drawer responsive to different screen sizes.

## Prerequisites

Before we begin, make sure you have Flutter installed on your machine and your preferred IDE set up.

## Step 1: Setting up the project

Create a new Flutter project by running the following command in your terminal:

```dart
flutter create responsive_drawer
```

Change directory to the project:

```dart
cd responsive_drawer
```

## Step 2: Creating the navigation drawer

In the `lib` folder, open `main.dart` and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Drawer'),
        ),
        drawer: MediaQuery.of(context).size.width > 600
            ? null
            : Drawer(
                child: ListView(
                  padding: EdgeInsets.zero,
                  children: <Widget>[
                    DrawerHeader(
                      child: Text('Navigation Drawer'),
                      decoration: BoxDecoration(
                        color: Colors.blue,
                      ),
                    ),
                    ListTile(
                      title: Text('Home'),
                      onTap: () {},
                    ),
                    ListTile(
                      title: Text('About'),
                      onTap: () {},
                    ),
                    ListTile(
                      title: Text('Settings'),
                      onTap: () {},
                    ),
                  ],
                ),
              ),
        body: Center(
          child: Text('Main Content'),
        ),
      ),
    );
  }
}
```

## Explanation

In the code above, we have created a `MyApp` widget, which serves as the root widget for our application.

In the `Scaffold` widget, we have added an `AppBar` as the top navigation bar and a `Drawer` as the side navigation drawer.

To make our navigation drawer responsive, we use `MediaQuery.of(context).size.width > 600` to check if the device width is greater than 600 pixels. If true, we render null instead of the drawer, which means the drawer will not be shown on larger screens.

Inside the `Drawer`, we have added a `ListView` with a `DrawerHeader` and three `ListTile` widgets for representing different menu options.

In the `body` of the `Scaffold`, we have added a sample text widget to represent the main content.

## Step 3: Run the app

Save the changes to `main.dart` and run the app using the following command:

```dart
flutter run
```

You should now see a responsive navigation drawer in your Flutter application. On smaller screens, the drawer will be accessible by swiping from the left side, while on larger screens, it will be hidden.

## Conclusion

In this tutorial, we learned how to create a responsive navigation drawer using `MediaQuery` in Flutter. By using `MediaQuery.of(context).size.width`, we can determine the screen size and conditionally show or hide the navigation drawer based on the screen width. This helps in creating a user-friendly interface that adapts to different device sizes.

#flutter #responsivedrawer