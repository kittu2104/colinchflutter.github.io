---
layout: post
title: "Implementing real-time location tracking in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In this tutorial, we will explore how to implement real-time location tracking in a MaterialApp, using the Flutter framework. By leveraging the device's GPS capabilities, we can continuously retrieve the user's location and display it in our application.

## Table of Contents

1. [Introduction](#introduction)
2. [Setting Up the Project](#setting-up-the-project)
3. [Getting User Location](#getting-user-location)
4. [Displaying the Location](#displaying-the-location)
5. [Updating the Location](#updating-the-location)
6. [Conclusion](#conclusion)

## Introduction<a name="introduction"></a>

Real-time location tracking has become a fundamental feature in many mobile applications. Whether it's for tracking delivery orders, finding nearby services, or enhancing social networking experiences, displaying accurate user location is essential.

## Setting Up the Project<a name="setting-up-the-project"></a>

To get started, create a new Flutter project and open it in your preferred code editor. Make sure you have the necessary dependencies by adding the following to your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  location: ^4.3.0
```

Run `flutter pub get` in your terminal to fetch and install the dependencies.

## Getting User Location<a name="getting-user-location"></a>

To retrieve the user's location, we will use the `location` package. Import it into your Dart file:

```dart
import 'package:location/location.dart';
```

Next, initialize a `Location` object and request permission to access the device's location:

```dart
Location location = Location();

if (await location.hasPermission() == PermissionStatus.denied) {
  await location.requestPermission();
}
```

Use the `getLocation()` method to retrieve the user's current location:

```dart
LocationData userLocation = await location.getLocation();
```

## Displaying the Location<a name="displaying-the-location"></a>

To display the user's location, we can use a widget provided by the Flutter framework. For simplicity, we will use a `Text` widget. Add the following code to your widget tree:

```dart
Text('Latitude: ${userLocation.latitude}, Longitude: ${userLocation.longitude}')
```

This will show the latitude and longitude of the user's location.

## Updating the Location<a name="updating-the-location"></a>

To continuously update the user's location, we can wrap the `getLocation()` method inside a periodic timer. This allows us to retrieve the location at regular intervals. Add the following code inside the `initState()` method of your `StatefulWidget`:

```dart
Timer.periodic(Duration(seconds: 10), (Timer t) async {
  userLocation = await location.getLocation();
  setState(() {});
});
```

This will update the `userLocation` variable and trigger a rebuild of the widget tree every 10 seconds.

## Conclusion<a name="conclusion"></a>

In this tutorial, we learned how to implement real-time location tracking in a MaterialApp using the Flutter framework. We explored how to retrieve the user's location, display it in the UI, and continuously update the location at regular intervals. By following these steps, you can create powerful location-aware applications.