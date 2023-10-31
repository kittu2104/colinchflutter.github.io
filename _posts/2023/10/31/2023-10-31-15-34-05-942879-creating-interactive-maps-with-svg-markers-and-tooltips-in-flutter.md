---
layout: post
title: "Creating interactive maps with SVG markers and tooltips in Flutter"
description: " "
date: 2023-10-31
tags: []
comments: true
share: true
---

Flutter is a powerful cross-platform framework for building mobile applications. It provides a wide range of widgets and plugins to create stunning user interfaces and interactive experiences. In this tutorial, we will explore how to create interactive maps with SVG markers and tooltips in Flutter.

## Table of Contents
- [Introduction](#introduction)
- [Setting up the Project](#setting-up-the-project)
- [Creating the Map](#creating-the-map)
- [Adding SVG Markers](#adding-svg-markers)
- [Adding Tooltips](#adding-tooltips)
- [Conclusion](#conclusion)

## Introduction

Interactive maps are a great way to display geographical information in your Flutter applications. They allow users to interact with the map, view specific locations, and obtain additional information.

In this tutorial, we will use Flutter's `flutter_svg` plugin to render SVG markers on a map and add tooltips to provide additional details about specific locations.

## Setting up the Project

To begin, open your Flutter project in your preferred IDE or text editor. Ensure that the `flutter_svg` plugin is added to your project by including it in the `pubspec.yaml` file:

```yaml
dependencies:
  flutter_svg: ^0.22.0
```

Run `flutter pub get` to fetch the plugin and its dependencies.

## Creating the Map

To create the map, we will use Flutter's `flutter_map` plugin, which integrates Leaflet maps into Flutter applications. Start by importing the required dependencies:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_map/flutter_map.dart';
import 'package:latlong2/latlong.dart';
```

Next, define a `MapController` and a list of `Marker`s that will be displayed on the map. Here's an example of how to create a basic map with a single marker:

```dart
MapController mapController = MapController();
List<Marker> markers = [
  Marker(
    point: LatLng(latitude, longitude),
    builder: (ctx) => Container(
      child: SvgPicture.asset(
        'assets/marker.svg',
        height: 30,
        width: 30,
      ),
    ),
  ),
];
```

Replace `latitude` and `longitude` with the actual coordinates of the marker.

To display the map, use the `FlutterMap` widget and configure it with your desired settings. Here's an example:

```dart
FlutterMap(
  mapController: mapController,
  options: MapOptions(
    center: LatLng(centerLatitude, centerLongitude),
    zoom: 10,
  ),
  layers: [
    TileLayerOptions(
      urlTemplate: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      subdomains: ['a', 'b', 'c'],
    ),
    MarkerLayerOptions(markers: markers),
  ],
)
```

Replace `centerLatitude` and `centerLongitude` with the desired center coordinates of the map.

## Adding SVG Markers

Now that we have a basic map with a marker, let's explore how to use SVG markers instead of the default icons.

First, make sure the SVG marker file is placed in the `assets` folder of your Flutter project.

To use an SVG marker, update the `builder` of the `Marker` widget to wrap the `SvgPicture.asset` widget with `SvgWidget` from the `flutter_svg` plugin:

```dart
import 'package:flutter_svg/flutter_svg.dart';

// ...

Marker(
  point: LatLng(latitude, longitude),
  builder: (ctx) => SvgWidget(
    child: SvgPicture.asset(
      'assets/marker.svg',
      height: 30,
      width: 30,
    ),
  ),
)
```

This will render the SVG marker on the map.

## Adding Tooltips

Tooltips provide additional information when a user interacts with a marker on the map. Let's see how to add tooltips to our SVG markers.

First, create a `StatefulWidget` to manage the tooltip visibility:

```dart
class MarkerTooltip extends StatefulWidget {
  final Widget child;

  const MarkerTooltip({Key? key, required this.child}) : super(key: key);

  @override
  _MarkerTooltipState createState() => _MarkerTooltipState();
}
```

In the `_MarkerTooltipState` class, manage the tooltip visibility using a `boolean` flag and handle the show/hide behavior:

```dart
class _MarkerTooltipState extends State<MarkerTooltip> {
  bool showTooltip = false;

  void toggleTooltip(bool value) {
    setState(() {
      showTooltip = value;
    });
  }

  @override
  Widget build(BuildContext context) {
    return GestureDetector(
      onTap: () => toggleTooltip(!showTooltip),
      child: Stack(
        children: [
          widget.child,
          if (showTooltip)
            Positioned(
              bottom: 0,
              // Add your tooltip widget here
              child: Container(
                // ...
              ),
            ),
        ],
      ),
    );
  }
}
```

Finally, wrap the marker widget with `MarkerTooltip` to enable tooltip functionality:

```dart
MarkerTooltip(
  child: SvgWidget(
    child: SvgPicture.asset(
      'assets/marker.svg',
      height: 30,
      width: 30,
    ),
  ),
)
```

You can customize the tooltip widget according to your requirements. Remember to update the `onTap` handler in the `GestureDetector` to trigger the tooltip visibility.

## Conclusion

Congratulations! You have learned how to create interactive maps with SVG markers and tooltips in Flutter. You can further enhance the map by customizing markers, adding animations, or integrating with APIs to fetch marker data dynamically. Flutter provides a wide range of plugins and widgets to help you create beautiful and interactive maps effortlessly.

Happy mapping!

---

References:
- [Flutter](https://flutter.dev/)
- [Flutter SVG Plugin](https://pub.dev/packages/flutter_svg)
- [Flutter Map Plugin](https://pub.dev/packages/flutter_map)