---
layout: post
title: "Creating a responsive floating action button using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [flutter, responsiveness]
comments: true
share: true
---

![Flutter Logo](https://flutter.dev/images/flutter-mark-square-100.png)

In this blog post, we will learn how to create a responsive floating action button (FAB) using `MediaQuery` in Flutter. The FAB is an essential component in many mobile app designs, and it is important to make it responsive to different screen sizes.

## Prerequisites
Before we proceed, make sure you have Flutter installed on your development machine. You can download and install Flutter from the official Flutter website at [https://flutter.dev](https://flutter.dev).

## Getting Started
Once you have Flutter installed, create a new Flutter project using your preferred IDE or the command line.

```dart
flutter create responsive_fab
cd responsive_fab
```

## Implementing the Responsive Floating Action Button
To create a responsive floating action button, we will use the `MediaQuery` class provided by Flutter. The `MediaQuery` class allows us to get information about the current device's screen size and orientation.

First, open the `lib/main.dart` file in your project directory. We will replace the default `MyHomePage` class with our implementation.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive FAB',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive FAB'),
        ),
        body: Center(
          child: Text(
            'Hello, World!',
            style: TextStyle(fontSize: 24),
          ),
        ),
        floatingActionButton: _buildFab(context),
      ),
    );
  }
  
  Widget _buildFab(BuildContext context) {
    final screenSize = MediaQuery.of(context).size;
    final isLargeScreen = screenSize.width >= 600;

    return FloatingActionButton(
      onPressed: () {
        // Add your FAB button action here
      },
      child: Icon(Icons.add),
      backgroundColor: isLargeScreen ? Colors.red : Colors.blue,
    );
  }
}
```

In the `MyApp` class, we have added the `_buildFab` method, which constructs our responsive FAB based on the screen size. The `MediaQuery` class allows us to obtain the screen size using `MediaQuery.of(context).size`. 

We then check if the screen width is greater than or equal to 600, and set the FAB's background color accordingly. In this example, we have used `Colors.red` for large screens and `Colors.blue` for smaller screens.

Finally, we set the `floatingActionButton` property of the `Scaffold` widget to the result of the `_buildFab` method.

## Testing the Responsive FAB
Save the changes to the `main.dart` file and run the app using the `flutter run` command. You should now see a responsive FAB with a red background on large screens and a blue background on smaller screens.

## Conclusion
In this blog post, we have learned how to create a responsive floating action button using `MediaQuery` in Flutter. By adapting the FAB's appearance based on the screen size, we can provide a better user experience across different devices.

Happy coding!

#flutter #UI #responsiveness