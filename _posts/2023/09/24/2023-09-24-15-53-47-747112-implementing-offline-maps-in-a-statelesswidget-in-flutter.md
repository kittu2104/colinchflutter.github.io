---
layout: post
title: "Implementing offline maps in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [OfflineMaps]
comments: true
share: true
---

In this blog post, we will explore how to implement offline maps in a stateless widget in Flutter using the [`flutter_map`](https://pub.dev/packages/flutter_map) package. Offline maps allow users to view maps and access location information even without an internet connection, making it ideal for scenarios like hiking, traveling, or areas with limited network connectivity.

## Setting Up

Before we begin, make sure you have Flutter and Dart installed. Create a new Flutter project and add the `flutter_map` dependency in your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  flutter_map: any
  # Add any other required dependencies
```

Then, run `flutter packages get` to fetch the package.

## Displaying Offline Maps

First, we need to import the necessary packages in our Dart file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_map/flutter_map.dart';
import 'package:latlong/latlong.dart';
```

Next, create a stateless widget for displaying the offline map:

```dart
class OfflineMapWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Offline Map'),
      ),
      body: FlutterMap(
        options: MapOptions(
          center: LatLng(51.5074, -0.1278), // Set the initial map location
          zoom: 13.0, // Set the initial zoom level
        ),
        layers: [
          TileLayerOptions(
            urlTemplate: 'assets/map/{z}/{x}/{y}.png', // Path to your offline tile images
            subdomains: ['a', 'b', 'c'], // Optional subdomains
          ),
        ],
      ),
    );
  }
}
```

Within the `FlutterMap` widget, we specify the `MapOptions` to set the initial map location and zoom level. We then define a `TileLayerOptions` with the `urlTemplate` pointing to the folder containing the offline tile images.

## Adding Offline Tiles

To display offline maps, we need to obtain the offline tiles beforehand. There are several ways to generate the tile images, including using tools like [Mobile Atlas Creator](https://mobac.sourceforge.io/) or open-source tile servers like [TileServer GL](https://tileserver.readthedocs.io/). Make sure to save the generated tiles in the correct folder structure following the `{z}/{x}/{y}.png` format.

Once you have the offline tiles ready, add them to your Flutter project's `assets` folder, and include them in the `pubspec.yaml` file:

```dart
flutter:
  assets:
    - assets/map/
```

Finally, run `flutter packages get` to fetch the new assets.

## Conclusion

Implementing offline maps in a StatelessWidget in Flutter is straightforward using the `flutter_map` package. By providing offline tiles, users can enjoy the benefits of viewing and navigating maps without an internet connection. This functionality is perfect for users who are frequently on the move or exploring remote areas where network connectivity may be limited.

Give it a try, and let us know how you used this feature in your Flutter project!

---

#Flutter #OfflineMaps