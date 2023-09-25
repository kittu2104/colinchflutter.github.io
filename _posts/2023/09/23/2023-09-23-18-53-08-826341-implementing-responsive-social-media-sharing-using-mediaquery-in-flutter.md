---
layout: post
title: "Implementing responsive social media sharing using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [responsivedesign]
comments: true
share: true
---

In today's digital world, social media sharing has become an integral part of any application. With the rise of smartphones and different screen sizes, it is important to make sure that social media sharing buttons are responsive and adapt to different device screens. In this tutorial, we will explore how to implement responsive social media sharing using `MediaQuery` in Flutter.

## Prerequisites

Before we start, make sure you have Flutter installed on your machine. If not, you can follow the installation guide [here](https://flutter.dev/docs/get-started/install).

## Step 1: Setting up the Project

Create a new Flutter project by running the following command in your terminal:

```bash
flutter create responsive_social_media_sharing
```

Once the project is created, navigate into the project folder:

```bash
cd responsive_social_media_sharing
```

## Step 2: Adding Dependencies

Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  share: ^2.0.2
```

This will allow us to use the `share` package to implement social media sharing functionality in our Flutter app. Save the `pubspec.yaml` file and run `flutter pub get` in your terminal to download the dependency.

## Step 3: Setting up the UI

Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:share/share.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Social Media Sharing',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Social Media Sharing'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'Share your App',
              style: TextStyle(
                fontSize: 20,
                fontWeight: FontWeight.bold,
              ),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                _shareContent(context);
              },
              child: Text('Share'),
            ),
          ],
        ),
      ),
    );
  }

  void _shareContent(BuildContext context) {
    Share.share('Check out this awesome app!');
  }
}
```

In this code, we have created a simple Flutter app with an app bar, a title, and a "Share" button in the center of the screen. We have used the `share` package to implement the `_shareContent` function, which shares the content using the native sharing functionality of the device.

## Step 4: Implementing Responsive Design

Now, let's make our social media sharing buttons responsive using `MediaQuery`. 

Update the `build` method of the `MyHomePage` class as follows:

```dart
@override
Widget build(BuildContext context) {
  final screenWidth = MediaQuery.of(context).size.width; // Get the screen width
  final buttonWidth = screenWidth > 600 ? 200.0 : 100.0; // Set the button width based on screen width
  final buttonTextSize = screenWidth > 600 ? 20.0 : 16.0; // Set the button text size based on screen width

  return Scaffold(
    appBar: AppBar(
      title: Text('Social Media Sharing'),
    ),
    body: Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: <Widget>[
          Text(
            'Share your App',
            style: TextStyle(
              fontSize: 20,
              fontWeight: FontWeight.bold,
            ),
          ),
          SizedBox(height: 20),
          SizedBox(
            width: buttonWidth,
            child: ElevatedButton(
              onPressed: () {
                _shareContent(context);
              },
              child: Text(
                'Share',
                style: TextStyle(fontSize: buttonTextSize),
              ),
            ),
          ),
        ],
      ),
    ),
  );
}
```

In this updated code, we use `MediaQuery` to retrieve the screen width (`screenWidth`). We then set the `buttonWidth` and `buttonTextSize` based on the screen width. If the screen width is greater than 600 (which indicates a tablet or larger screen), we set the button width to 200 and the button text size to 20. Otherwise, we set the values to 100 and 16 respectively.

## Step 5: Run the App

Save the changes and run the app using the following command:

```bash
flutter run
```

You should now see the responsive social media sharing buttons in the app. The button width and text size will adapt based on the screen width of the device.

Congratulations! You have successfully implemented responsive social media sharing using `MediaQuery` in Flutter.

## Conclusion

In this tutorial, we learned how to implement responsive social media sharing buttons in Flutter using `MediaQuery`. By adapting the width and text size of the buttons based on the screen width, we ensure a better user experience across different devices. Now you can make your Flutter app's social media sharing buttons responsive and provide an optimized experience to your users.

#flutter #responsivedesign