---
layout: post
title: "Creating splash screens with MaterialApp."
description: " "
date: 2023-10-23
tags: [loading]
comments: true
share: true
---

When creating mobile apps, it is common to have a splash screen that is shown when the app is launched. A splash screen can provide a professional and polished look to your app, while also giving the app time to load its initial resources.

In Flutter, we can easily create a splash screen using the `MaterialApp` widget. The `MaterialApp` is the main entry point of your app and allows you to customize various aspects of your app's appearance and behavior, including the splash screen.

To create a splash screen with `MaterialApp`, follow these steps:

## Step 1: Create a Splash Screen Widget

First, we need to create a widget that represents our splash screen. This widget will be displayed until your app finishes loading and is ready to show its content. Here's an example of a simple splash screen widget:

```dart
class SplashScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Image.asset('assets/splash.png'),
      ),
    );
  }
}
```

In this example, we use the `Image.asset` widget to display an image as the splash screen. You can replace it with any widget you like to customize your splash screen's appearance.

## Step 2: Specify the Splash Screen in MaterialApp

Next, we will integrate our splash screen into the `MaterialApp` widget in your app's `main.dart` file. Here's an example:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: SplashScreen(),
      // ... other properties and routes
    );
  }
}
```

In this example, we set the `home` property of `MaterialApp` to our splash screen widget, `SplashScreen()`. This tells the `MaterialApp` to display the splash screen widget when the app is launched.

## Step 3: Handle App Load and Navigate to Main Screen

After the splash screen has been displayed for a certain duration or after your app finishes loading its resources, you can navigate to the main screen of your app. To do this, you can use `Navigator` from within your splash screen widget.

Here's an example of how to navigate to the main screen after a 2-second delay:

```dart
class SplashScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    Future.delayed(Duration(seconds: 2), () {
      Navigator.of(context).pushReplacement(
        MaterialPageRoute(builder: (context) => MainScreen()),
      );
    });

    return Scaffold(
      body: Center(
        child: Image.asset('assets/splash.png'),
      ),
    );
  }
}
```

In this example, we use `Navigator.of(context).pushReplacement` to replace the splash screen with the `MainScreen` widget. This ensures that the splash screen is disposed of and won't be accessible when the user presses the back button.

That's it! You have now successfully created a splash screen using the `MaterialApp` widget in Flutter. Customize the splash screen widget and add any additional logic as per your app's requirements.

# Conclusion

Adding a splash screen to your app can enhance the user experience and provide a professional feel. Flutter makes it easy to create and integrate a splash screen using the `MaterialApp` widget. By following the steps outlined in this tutorial, you can create a splash screen that ensures a smooth and visually appealing start to your app.

**References:**
- [Flutter Documentation on MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter Navigator Documentation](https://api.flutter.dev/flutter/widgets/Navigator-class.html)
- [Flutter Widgets Catalog - Image](https://flutter.dev/docs/development/ui/widgets/assets#loading-images)