---
layout: post
title: "Implementing geolocation updates with background services in Flutter"
description: " "
date: 2023-10-25
tags: []
comments: true
share: true
---

In today's digital world, location-based services have become an integral part of mobile application development. Flutter, being a versatile framework, provides various options to implement geolocation updates in your application. One of the efficient ways to ensure continuous location updates, even when the app is in the background, is by utilizing background services.

In this article, we will explore how to implement geolocation updates using background services in Flutter.

## Table of Contents
1. [Introduction](#introduction)
2. [Setting up Dependencies](#dependencies)
3. [Implementing Geolocation Service](#geolocation-service)
4. [Setting Up Background Execution](#background-execution)
5. [Testing the Geolocation Updates](#testing-updates)
6. [Conclusion](#conclusion)

## Introduction<a name="introduction"></a>

Geolocation updates can be crucial for various applications such as tracking, navigation, and location-based notifications. Flutter provides a plugin called `geolocator` that allows easy integration with native geolocation services on both Android and iOS platforms. However, to ensure continuous updates even when the app is in the background, we need to leverage background services.

## Setting up Dependencies<a name="dependencies"></a>

To get started, add the `geolocator` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  geolocator: any
```

Then, run `flutter pub get` to fetch the package.

## Implementing Geolocation Service<a name="geolocation-service"></a>

Create a new Dart file, `geolocation_service.dart`, in your project. This file will hold the code responsible for fetching geolocation updates. Here's an example of how you can structure the file:

```dart
import 'package:geolocator/geolocator.dart';

class GeolocationService {
  final Geolocator _geolocator = Geolocator();

  Future<Position> getCurrentPosition() async {
    return await _geolocator.getCurrentPosition(
      desiredAccuracy: LocationAccuracy.best,
    );
  }

  Stream<Position> getGeolocationUpdates() {
    return _geolocator.getPositionStream(
      desiredAccuracy: LocationAccuracy.best,
      distanceFilter: 10, // In meters
    );
  }
}
```

The `getCurrentPosition()` function retrieves the current user position, while `getGeolocationUpdates()` returns a continuous stream of position updates with a specified accuracy and distance filter.

## Setting Up Background Execution<a name="background-execution"></a>

To enable background execution in your Flutter app, you'll need to handle platform-specific implementations on both Android and iOS. Follow these steps to configure background execution:

### On Android:

1. Open the `AndroidManifest.xml` file located in the `android/app/src/main` directory.
2. Add the following permissions inside the `<manifest>` tag:

```xml
<uses-permission android:name="android.permission.FOREGROUND_SERVICE"/>
<uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
```

3. Inside the `<application>` tag, add the following service:

```xml
<service
   android:name="com.lyokone.location.LocationBroadcastReceiver"
   android:exported="false"/>
```

### On iOS:

1. Open the `Info.plist` file located in the `ios/Runner` directory.
2. Add the following keys:

```xml
<key>UIBackgroundModes</key>
<array>
   <string>fetch</string>
   <string>location</string>
</array>
```

3. Inside the `<dict>` tag, add this key-value pair:

```xml
<key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
<string>Your location is required to provide accurate results.</string>
```

## Testing the Geolocation Updates<a name="testing-updates"></a>

To test the geolocation updates, you can use a simple Flutter layout with corresponding code. For example:

```dart
import 'dart:async';

import 'package:flutter/material.dart';
import 'package:geolocator/geolocator.dart';

import 'geolocation_service.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Geolocation Service Demo',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Geolocation Service Demo'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              ElevatedButton(
                onPressed: _getCurrentLocation,
                child: Text('Get Current Location'),
              ),
              SizedBox(height: 20),
              StreamBuilder<Position>(
                stream: GeolocationService().getGeolocationUpdates(),
                builder: (context, snapshot) {
                  if (snapshot.hasData) {
                    final position = snapshot.data!;
                    return Text(
                      'Latitude: ${position.latitude}, Longitude: ${position.longitude}',
                    );
                  }

                  return Text('Waiting for location updates');
                },
              ),
            ],
          ),
        ),
      ),
    );
  }

  Future<void> _getCurrentLocation() async {
    final position = await GeolocationService().getCurrentPosition();
    print('Current Position: ${position.latitude}, ${position.longitude}');
  }
}
```

Running the above example, you will be able to fetch the current location by tapping the "Get Current Location" button. Meanwhile, the continuous geolocation updates will be displayed below.

## Conclusion<a name="conclusion"></a>

Implementing geolocation updates with background services in Flutter is essential when you need continuous location updates, even when the app is in the background. Utilizing the `geolocator` package and configuring background execution on both Android and iOS platforms, you can easily implement geolocation services in your Flutter applications.

Remember to handle permissions and provide clear explanations to the user regarding the usage of their location data.

Now that you have learned how to implement geolocation updates with background services in Flutter, you can enhance your apps with advanced features that rely on accurate location information. Happy coding!

**References:**

- Flutter Geolocator Plugin: [https://pub.dev/packages/geolocator](https://pub.dev/packages/geolocator)
- Flutter Official Documentation on Background Execution: [https://flutter.dev/docs/development/packages-and-plugins/background-processes](https://flutter.dev/docs/development/packages-and-plugins/background-processes)