---
layout: post
title: "Using Google Maps in MaterialApp."
description: " "
date: 2023-10-23
tags: [googlemaps]
comments: true
share: true
---

In this blog post, we will explore how to integrate Google Maps into a `MaterialApp` in a Flutter application. Google Maps provides a powerful mapping library that can be utilized to display maps, locate addresses, add markers, and much more.

## Prerequisites

Before we begin, make sure you have the following prerequisites:

- Knowledge of Flutter and Dart
- Flutter SDK installed
- A text editor (such as Visual Studio Code)

## Step 1: Setup Google Maps API Key

To use Google Maps in your Flutter application, you need to obtain an API key from the Google Cloud Platform Console. Follow these steps to get your API key:

1. Go to the [Google Cloud Platform Console](https://console.cloud.google.com/) and create a new project or select an existing one.
2. Enable the **Maps SDK for Android** and the **Maps SDK for iOS** for your project.
3. Go to the **Credentials** page and create a new API key.
4. Make sure the API key has the required permissions for using Google Maps.

## Step 2: Add required dependencies

Open your Flutter project in your preferred text editor and navigate to the `pubspec.yaml` file. Add the following dependencies under the `dependencies` section:

```dart
dependencies:
  flutter:
    sdk: flutter
  google_maps_flutter: ^1.0.0
```

Save the file and run the following command in the terminal to fetch the new dependencies:

```bash
flutter pub get
```

## Step 3: Implement Google Maps in MaterialApp

Open your main application file (e.g., `main.dart`) and import the required packages:

```dart
import 'package:flutter/material.dart';
import 'package:google_maps_flutter/google_maps_flutter.dart';
```

Inside the `build` method of your `MaterialApp`, create an instance of `GoogleMap` and provide your API key as follows:

```dart
GoogleMap(
  initialCameraPosition: CameraPosition(
    target: LatLng(37.42796133580664, -122.085749655962),
    zoom: 14,
  ),
  markers: {
    Marker(
      markerId: MarkerId('marker_id'),
      position: LatLng(37.42796133580664, -122.085749655962),
      infoWindow: InfoWindow(title: 'Googleplex'),
    ),
  },
  onMapCreated: (GoogleMapController controller) {
    // Optional: Perform additional operations on map creation
  },
)
```

Replace the `target` coordinates with the initial position you want to display on the map. You can also customize the markers according to your needs.

Finally, run your application using the following command:

```bash
flutter run
```

## Conclusion

By following the steps outlined in this blog post, you should now be able to integrate Google Maps into your MaterialApp in Flutter. You can explore more options and functionalities offered by the Google Maps API to enhance your application's mapping experience.

If you face any issues or have any questions, please refer to the official [Google Maps documentation](https://developers.google.com/maps/documentation) for more information.

Happy mapping! 

**#flutter #googlemaps**