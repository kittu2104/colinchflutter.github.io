---
layout: post
title: "Implementing maps and geolocation in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [flutter, maps, geolocation]
comments: true
share: true
---

## Introduction

Maps and geolocation are important features in many mobile applications. They allow users to view and interact with maps, as well as retrieve their current location. In this blog post, we will explore how to implement maps and geolocation in a StatelessWidget using Flutter, a popular cross-platform mobile app development framework.

## Prerequisites

Before we begin, make sure you have the following:

- Installed Flutter SDK
- Integrated development environment (IDE) such as Visual Studio Code or Android Studio
- Basic knowledge of Flutter and Dart programming

## Step 1: Adding Dependencies

To implement maps and geolocation in your Flutter project, you need to add the following dependencies to your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  google_maps_flutter: ^2.0.4
  geolocator: ^7.6.2
```

The `google_maps_flutter` package provides map rendering capabilities, while the `geolocator` package allows you to retrieve the current location of the device.

## Step 2: Implementing the Widget

Create a new `StatelessWidget` called `MapWidget`. Then, import the required packages:

```dart
import 'package:flutter/material.dart';
import 'package:google_maps_flutter/google_maps_flutter.dart';
import 'package:geolocator/geolocator.dart';
```

Within the `MapWidget` class, define a `GoogleMapController` and a `CameraPosition` to control the map view:

```dart
class MapWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final CameraPosition initialPosition = CameraPosition(
      target: LatLng(0, 0),
      zoom: 10,
    );

    GoogleMapController mapController;

    return Container(
      child: GoogleMap(
        initialCameraPosition: initialPosition,
        onMapCreated: (controller) {
          mapController = controller;
        },
      ),
    );
  }
}
```

## Step 3: Requesting User Permission

Add a method called `checkLocationPermission()` inside the `MapWidget` class to request user permission for accessing their location:

```dart
Future<bool> checkLocationPermission() async {
  LocationPermission permission = await Geolocator.checkPermission();

  if (permission == LocationPermission.denied) {
    permission = await Geolocator.requestPermission();
    if (permission == LocationPermission.denied ||
        permission == LocationPermission.deniedForever) {
      return false;
    }
  }

  return true;
}
```

## Step 4: Retrieving User Location

Add another method called `getUserLocation()` to fetch the user's current location:

```dart
Future<LatLng> getUserLocation() async {
  Position position = await Geolocator.getCurrentPosition(
    desiredAccuracy: LocationAccuracy.high,
  );

  return LatLng(position.latitude, position.longitude);
}
```

## Step 5: Updating Camera Position

Update the `onMapCreated` callback function in the `GoogleMap` widget to center the map on the user's current location:

```dart
onMapCreated: (controller) async {
    mapController = controller;
    bool hasPermission = await checkLocationPermission();

    if (hasPermission) {
        LatLng userLocation = await getUserLocation();
        mapController.animateCamera(
            CameraUpdate.newLatLng(userLocation),
        );
    }
},
```

## Step 6: Adding the MapWidget

Finally, you can now add the `MapWidget` to any screen or widget tree in your Flutter application:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('My Map App'),
        ),
        body: MapWidget(),
      ),
    );
  }
}
```

## Conclusion

In this blog post, we have learned how to implement maps and geolocation in a `StatelessWidget` using Flutter. By following the steps outlined, you can easily create apps that include interactive maps and location-based features. Remember to test your app on different devices and handle any potential errors related to geolocation permissions.

#flutter #maps #geolocation