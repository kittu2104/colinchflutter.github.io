---
layout: post
title: "Implementing geofencing in scheduled tasks with WorkManager in Flutter"
description: " "
date: 2023-10-01
tags: [geofencing, workmanager]
comments: true
share: true
---

![Geofencing](https://example.com/geofencing_image.jpg)

Geofencing is a powerful technique that allows you to define virtual boundaries and trigger specific actions when a user enters or exits those boundaries. It has a wide range of applications, from location-based reminders to tracking user movement.

In this tutorial, we'll explore how to implement geofencing in scheduled tasks using WorkManager in Flutter. WorkManager is a background processing library that allows you to schedule tasks efficiently and reliably.

## Prerequisites
To follow this tutorial, you'll need the following:
- Flutter SDK installed on your machine
- Android Studio or IntelliJ IDEA with the Flutter plugin
- Basic understanding of Flutter and Dart programming language

Let's get started!

## Step 1: Set up WorkManager
First, we need to set up WorkManager in our Flutter project. Open your `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter_workmanager: ^2.0.0
  location: ^4.2.0
```

Save the file and run `flutter pub get` to install the dependencies.

## Step 2: Request Location Permissions
Geofencing requires access to the user's location. To do this, we'll utilize the `location` package. Open your `AndroidManifest.xml` file located in `android/app/src/main` and add the following lines inside the `<manifest>` tag:

```xml
<manifest ...>
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
    
    <!-- ... -->
</manifest>
```

Next, open your `Info.plist` file located in `ios/Runner` and add the following lines:

```xml
<plist version="1.0">
    <dict>
        <!-- ... -->
        
        <key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
        <string>Allow access to your location</string>
        <key>NSLocationWhenInUseUsageDescription</key>
        <string>Allow access to your location</string>
        <key>NSLocationAlwaysUsageDescription</key>
        <string>Allow access to your location</string>
        
        <!-- ... -->
    </dict>
</plist>
```

## Step 3: Implement Geofencing
Now, let's implement geofencing using `flutter_workmanager` and `location` packages. Create a new file, for example, `geofence_manager.dart`, and add the following code:

```dart
import 'package:flutter_workmanager/flutter_workmanager.dart';
import 'package:location/location.dart';

class GeofenceManager {
  static init() {
    FlutterWorkManager.initialize(callbackDispatcher);
    FlutterWorkManager.registerPeriodicTask(
      "geofencing_task",
      "geofencingTask",
      frequency: Duration.hours(1),
    );
  }

  static Future<void> geofencingTask() async {
    final location = Location();

    if (!(await location.serviceEnabled())) {
      return;
    }

    final hasPermission = await location.hasPermission();
    if (hasPermission == PermissionStatus.denied) {
      return;
    }

    final geofence = GeofenceRegion(
      id: "work_location",
      lat: 37.422,
      lng: -122.084,
    );

    final currentLocation = await location.getLocation();

    final distance = location.distanceBetween(
      currentLocation.latitude,
      currentLocation.longitude,
      geofence.lat,
      geofence.lng,
    );

    if (distance < 100) {
      // Perform desired action within workmanager task
      // E.g., send a notification, fetch data, etc.
    }

    FlutterWorkManager.cancelAll();
  }
}
```

## Step 4: Schedule Geofencing Task
To schedule the geofencing task, call the `init()` method from your `main.dart` file. Your `main.dart` should look something like this:

```dart
import 'package:flutter/material.dart';
import 'package:your_app/geofence_manager.dart';

void main() {
  runApp(MyApp());
  GeofenceManager.init();
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Your App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Center(
        child: Text(
          'Welcome to your app!',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

## Step 5: Test the Geofencing Task
Now it's time to test our geofencing task. Install the app on your Android device or emulator, and make sure you have the necessary location permissions enabled.

When the device is within 100 meters of the specified latitude and longitude coordinates, the desired action within the WorkManager task will be triggered.

## Conclusion
In this tutorial, you learned how to implement geofencing in scheduled tasks using WorkManager in Flutter. With geofencing, you can easily add location-based functionality to your Flutter app and perform specific actions based on the user's location.

Remember to test your app thoroughly and handle any permission-related requirements properly. Happy coding!

#flutter #geofencing #workmanager