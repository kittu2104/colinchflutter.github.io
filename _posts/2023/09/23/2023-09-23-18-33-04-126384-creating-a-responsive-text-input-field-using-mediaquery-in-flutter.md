---
layout: post
title: "Creating a responsive text input field using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [responsivedesign]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive text input field using the `MediaQuery` class in Flutter. Responsive design is crucial in today's fast-paced digital world, where users access applications on various screen sizes and devices. With Flutter's `MediaQuery` class, we can dynamically adjust the size of UI components based on the device's screen dimensions.

## Step 1: Setting up the Flutter Project

To get started, make sure you have Flutter installed on your machine. If you haven't installed Flutter yet, please refer to the official Flutter documentation to set it up.

Create a new Flutter project using the following command:

```
flutter create responsive_textfield
```

## Step 2: Updating the Default Flutter App

Open the `main.dart` file inside the `lib` directory and update the `build` method of the `MyApp` class. Replace the existing code with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive TextField',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive TextField'),
        ),
        body: Center(
          child: Container(
            padding: EdgeInsets.symmetric(horizontal: 16),
            width: MediaQuery.of(context).size.width * 0.8,
            child: TextField(
              decoration: InputDecoration(
                labelText: 'Enter text',
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

## Step 3: Understanding the Code

In the updated code, we have used the `MediaQuery` class to adjust the width of the `TextField` based on the device's screen size. The `MediaQuery.of(context).size.width` returns the total width of the screen, and we have multiplied it by 0.8 to make the `TextField` take up 80% of the screen width.

We have also wrapped the `TextField` inside a `Container` widget to provide some padding on the left and right sides using `EdgeInsets.symmetric(horizontal: 16)`.

## Step 4: Running the App

Save the changes and run the app using the following command:

```
flutter run
```

You should see a simple app with a responsive text input field. Try running the app on different devices or screen sizes, and you'll notice that the text field adjusts its width accordingly.

## Conclusion

In this tutorial, we have learned how to create a responsive text input field using the `MediaQuery` class in Flutter. By utilizing the device's screen dimensions, we can ensure that our UI components adapt to different screen sizes and provide a seamless user experience.

#flutter #responsivedesign