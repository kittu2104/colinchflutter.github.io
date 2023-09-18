---
layout: post
title: "Integration of Flutter Alarm Manager with Google Maps API"
description: " "
date: 2023-09-18
tags: [android]
comments: true
share: true
---

In this blog post, we will explore how to integrate the Flutter Alarm Manager plugin with the Google Maps API to create location-based alarms in Flutter applications.

## Prerequisites
Before we start, make sure you have Flutter and Dart installed on your machine. Additionally, you should have a basic understanding of Flutter development and how to create a new Flutter project.

## Installing Required Packages
To implement the integration, we need to install two dependencies: `flutter_alarm_manager` and `google_maps_flutter`.

To install these packages, add the following lines to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_alarm_manager: ^2.0.0
  google_maps_flutter: ^2.0.9
```

Then, run `flutter pub get` to download and install the packages.

## Setting up Google Maps API
To use the Google Maps API, you need to create a project on the Google Cloud Platform and enable the necessary APIs.

1. Open the [Google Cloud Console](https://console.cloud.google.com/) and create a new project.
2. Enable the **Maps SDK for Android** and **Maps SDK for iOS** APIs for your project.
3. Generate API keys for both Android and iOS.
4. Restrict your API keys to the specific usage domain, if required.

## Implementing the Integration
1. Create a new Flutter project by running `flutter create location_alarm`.
2. Open the `lib/main.dart` file in your project and replace its content with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';
import 'package:google_maps_flutter/google_maps_flutter.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Location Alarm',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  AlarmManager _alarmManager = AlarmManager();

  @override
  void initState() {
    super.initState();
    _setupLocationAlarm();
  }

  void _setupLocationAlarm() {
    final LatLng targetLocation = LatLng(37.422, -122.084); // Replace with your desired location
      
    _alarmManager.addLocationAlarm(
      targetLatitude: targetLocation.latitude,
      targetLongitude: targetLocation.longitude,
      radius: 1000, // Set the proximity radius in meters
      onEnter: () {
        // Handle alarm triggered when entering the target location
        // You can trigger a notification or perform any desired action here
      },
      onExit: () {
        // Handle alarm triggered when exiting the target location
      },
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Location Alarm'),
      ),
      body: Center(
        child: Text('Location Alarm Example'),
      ),
    );
  }
}
```

3. Replace the `targetLatitude` and `targetLongitude` values in the `_setupLocationAlarm` method with the coordinates of your desired location.
4. Run the Flutter application using `flutter run`.

## Conclusion
By following this guide, you have successfully integrated the Flutter Alarm Manager plugin with the Google Maps API to create location-based alarms in your Flutter application. You can now customize the alarm actions to fit your application's needs.

#flutter #android #googlemapsAPI #flutteralarmmanager