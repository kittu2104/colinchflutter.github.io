---
layout: post
title: "Working with ARKit and ARCore using GetX in Flutter"
description: " "
date: 2023-09-29
tags: []
comments: true
share: true
---

Augmented reality (AR) has become an exciting technology that allows developers to create engaging experiences in various industries. Flutter, Google's UI toolkit for building beautiful, natively compiled applications for mobile, web, and desktop from a single codebase, supports ARKit (for iOS) and ARCore (for Android) through various plugins. In this article, we will explore how to work with ARKit and ARCore using the popular state management package, GetX.

## What is GetX?

GetX is a lightweight and powerful package for state management, navigation, and dependency injection in Flutter applications. It simplifies the development process and provides a clean and scalable architecture. By leveraging GetX, we can easily integrate ARKit and ARCore functionality into our Flutter app.

## Setting up ARKit and ARCore

To get started, we need to add the necessary plugins to our Flutter project. The `arkit_flutter` plugin is used for ARKit, while the `arcore_flutter_plugin` plugin is used for ARCore. Open your project's `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  arkit_flutter: ^0.7.0
  arcore_flutter_plugin: ^1.2.0
  get: ^4.1.4
    # add any other dependencies your project uses
```

After adding the dependencies, run `flutter pub get` in your terminal to fetch the packages.

## Implementing ARKit and ARCore using GetX

Now that we have the plugins set up, we can start implementing ARKit and ARCore functionality using GetX. First, let's define a controller class that will handle the AR-related logic and state management. Create a new file called `ar_controller.dart` and add the following code:

```dart
import 'package:get/get.dart';
import 'package:arkit_plugin/arkit_plugin.dart';
import 'package:arcore_flutter_plugin/arcore_flutter_plugin.dart';

class ARController extends GetxController {
  ARPlatform _platform;
  ARController() {
    _initAR();
  }

  Future<void> _initAR() async {
    if (await ARPlatform.isARKitAvailable()) {
      _platform = ARPlatform.ARKit;
    } else if (await ARPlatform.isARCoreAvailable()) {
      _platform = ARPlatform.ARCore;
    }
    // Initialize ARKit or ARCore based on platform
    // Add your AR specific setup here
  }

  void placeObject() {
    // Implement object placement logic here
  }
}
```

In the code above, we define an `ARController` class that extends `GetXController` from GetX package. This controller handles the initialization of ARKit and ARCore based on the available platform. You can add any AR-specific setup code inside the `_initAR` method, like lighting, environment, or object loading.

Next, let's create a simple UI for our AR experience. Create a new file called `ar_page.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'ar_controller.dart';

class ARPage extends StatelessWidget {
  final ARController _controller = Get.put(ARController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('AR Page'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () => _controller.placeObject(), // Call placeObject method
          child: Text('Place Object'),
        ),
      ),
    );
  }
}
```

In the code above, we create an `ARPage` widget that extends `StatelessWidget`. Inside the `build` method, we instantiate `ARController` using `Get.put` from GetX package to initialize the controller and make it available to our widget. We then create a simple UI with a button that calls the `placeObject` method when pressed.

To use `ARPage`, update your `main.dart` file as follows:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'ar_page.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return GetMaterialApp(
      title: 'AR Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: ARPage(),
    );
  }
}
```

We wrap our `ARPage` inside a `GetMaterialApp` instead of the regular `MaterialApp` to enable GetX navigation and state management features.

## Conclusion

In this article, we explored how to work with ARKit and ARCore using GetX in Flutter. You can now create AR experiences and manage AR-related logic using the GetX package, making your development process more streamlined and maintainable. Augmented reality opens up a world of possibilities, and with Flutter and GetX, you can easily incorporate it into your own applications.

## #AR #Flutter