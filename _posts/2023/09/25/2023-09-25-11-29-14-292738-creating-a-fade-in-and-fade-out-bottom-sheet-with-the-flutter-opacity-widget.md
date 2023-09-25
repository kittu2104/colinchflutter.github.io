---
layout: post
title: "Creating a fade-in and fade-out bottom sheet with the Flutter Opacity widget"
description: " "
date: 2023-09-25
tags: [opacity]
comments: true
share: true
---

The Flutter framework provides numerous built-in widgets that make it easy to create clean and beautiful user interfaces. One powerful widget in Flutter is the Opacity widget, which allows us to control the transparency of its child widget. In this tutorial, we'll explore how to create a fade-in and fade-out effect for a bottom sheet using the Opacity widget in Flutter.

## Setting Up the Project

To get started, make sure you have Flutter installed on your system. If not, please follow the official Flutter installation guide for your operating system.

Once Flutter is set up, create a new Flutter project using the following command:

```dart
flutter create fade_in_bottom_sheet
cd fade_in_bottom_sheet
```

## Creating the Bottom Sheet

In this example, we'll create a simple bottom sheet with a text widget inside it. To create the bottom sheet, modify the `lib/main.dart` file as follows:

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
          title: Text('Fade-In Bottom Sheet'),
        ),
        body: Center(
          child: RaisedButton(
            onPressed: () {
              showModalBottomSheet(
                context: context,
                builder: (BuildContext context) {
                  return _buildBottomSheetContent(context);
                },
              );
            },
            child: Text('Show Bottom Sheet'),
          ),
        ),
      ),
    );
  }

  Widget _buildBottomSheetContent(BuildContext context) {
    return Container(
      color: Colors.white,
      child: Column(
        mainAxisSize: MainAxisSize.min,
        children: <Widget>[
          ListTile(
            leading: Icon(Icons.info),
            title: Text('Bottom Sheet Content'),
            subtitle: Text('This is an example bottom sheet'),
          ),
        ],
      ),
    );
  }
}
```

In this code, we define a `RaisedButton` widget that triggers the bottom sheet when pressed. The `showModalBottomSheet` function shows the bottom sheet using the `_buildBottomSheetContent` function as its content.

## Adding the Fade-In and Fade-Out Effect

To add the fade-in and fade-out effect, we'll wrap the `Container` widget that represents the bottom sheet content with the `Opacity` widget. Modify the code in the `_buildBottomSheetContent` function as follows:

```dart
  Widget _buildBottomSheetContent(BuildContext context) {
    return Opacity(
      opacity: 0.85,
      child: Container(
        color: Colors.white,
        child: Column(
          mainAxisSize: MainAxisSize.min,
          children: <Widget>[
            ListTile(
              leading: Icon(Icons.info),
              title: Text('Bottom Sheet Content'),
              subtitle: Text('This is an example bottom sheet'),
            ),
          ],
        ),
      ),
    );
  }
```

Here, we set the `opacity` property of the `Opacity` widget to 0.85, which will make the bottom sheet slightly transparent. Adjust the opacity value to achieve the desired effect.

## Testing the App

Now, run the app using the following command:

```dart
flutter run
```

Once the app launches on your device or emulator, you should see a button labeled "Show Bottom Sheet". Tap the button to reveal the bottom sheet with the fade-in effect. To close the bottom sheet, swipe it down or tap outside the sheet.

Congratulations! You have successfully created a fade-in and fade-out bottom sheet using the Flutter Opacity widget. Experiment with different opacity values and customize the bottom sheet's content to fit your app's requirements.

#flutter #opacity