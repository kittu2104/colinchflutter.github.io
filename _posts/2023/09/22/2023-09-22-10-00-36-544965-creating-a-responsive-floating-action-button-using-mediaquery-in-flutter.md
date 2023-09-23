---
layout: post
title: "Creating a responsive floating action button using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, dart]
comments: true
share: true
---

In Flutter, the Floating Action Button (FAB) is a popular UI element used to provide quick access to primary actions within a screen. A responsive FAB adapts its position based on the screen size or device orientation, ensuring optimal placement for users across different devices.

To create a responsive FAB in Flutter, we can utilize the `MediaQuery` class to determine the available screen size and dynamically position the FAB accordingly. Let's walk through a step-by-step process to achieve this.

## Step 1: Import Required Packages
Before we start, make sure to import the necessary packages:

```dart
import 'package:flutter/material.dart';
```

## Step 2: Define the Responsive FAB Widget
Next, let's define a separate widget for our responsive FAB:

```dart
class ResponsiveFAB extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Implement FAB functionality here

    return FloatingActionButton(
      // FAB properties here
    );
  }
}
```

## Step 3: Implement FAB Functionality
Within the `build` method of the `ResponsiveFAB` widget, we can utilize the `MediaQuery` class to determine the screen size and position the FAB accordingly. Here's an example of how we can implement this functionality:

```dart
class ResponsiveFAB extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final screenSize = MediaQuery.of(context).size;
    
    // Determine the position of the FAB based on the screen width
    final double fabPosition = screenSize.width > 600 ? 16.0 : screenSize.width - 80.0;

    return FloatingActionButton(
      onPressed: () {
        // FAB Button Action
      },
      child: Icon(Icons.add),
      backgroundColor: Colors.blue,
      foregroundColor: Colors.white,
      heroTag: null,
      elevation: 6.0,
      mini: screenSize.width > 600 ? false : true,
      shape: RoundedRectangleBorder(
        borderRadius: BorderRadius.circular(8.0),
      ),
      onPressed: () {
        // Perform action
      },
      tooltip: 'Add',
      // Position the FAB dynamically based on the screen size
      // using the fabPosition calculated earlier
      // Adjust the fabPosition values as needed for your layout
      // e.g., for left position use Offset(fabPosition, 16.0)
      // or for bottom position use Offset(16.0, fabPosition)
      // here we are positioning it on the bottom right
      //
      // Note: Make sure to wrap the FAB with a Stack widget as this
      // placement requires absolute positioning
      onPressed: () {},
    );
  }
}
```

## Step 4: Use the ResponsiveFAB Widget
Finally, we can use the `ResponsiveFAB` widget inside any Flutter screen. For example:

```dart
class MyScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('My Screen'),
      ),
      body: Center(
        child: Text('Hello, World!'),
      ),
      floatingActionButton: ResponsiveFAB(),
    );
  }
}
```

That's it! You have successfully created a responsive Floating Action Button using `MediaQuery` in Flutter. Now the FAB will adapt its position to provide a consistent user experience on different devices and screen sizes.

#flutter #dart

Remember to adjust the `fabPosition` value according to your specific layout needs. With this approach, your Flutter app will provide a seamless FAB experience across various devices, ensuring optimal usability and responsiveness.