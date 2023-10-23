---
layout: post
title: "Using device sensors in MaterialApp."
description: " "
date: 2023-10-23
tags: [sensors, sensors]
comments: true
share: true
---

In modern smartphones and tablets, various sensors are available, such as accelerometer, gyroscope, magnetometer, and proximity sensor. These sensors provide valuable information about the device's position, movement, and surroundings. In this blog post, we will explore how to use these device sensors in a MaterialApp.

## Table of Contents
- [Getting Sensor Data](#getting-sensor-data)
- [Using Sensor Data in MaterialApp](#using-sensor-data-in-materialapp)
- [Conclusion](#conclusion)

## Getting Sensor Data

To access device sensors in a Flutter application, we can use the `sensors` package, which provides an interface to interact with the sensors seamlessly. First, add the `sensors` package to your `pubspec.yaml` file:

```yaml
dependencies:
  sensors: ^0.5.0
```

Next, run the `flutter pub get` command to install the package in your Flutter project.

To use the accelerometer sensor, import the package and register a listener to receive accelerometer events:

```dart
import 'package:sensors/sensors.dart';

void main() {
  accelerometerEvents.listen((AccelerometerEvent event) {
    // Process accelerometer data
    double x = event.x;
    double y = event.y;
    double z = event.z;
    
    // Use the data for further calculations or UI updates
  });
}
```

Similarly, you can use other sensors like gyroscope or magnetometer by replacing `accelerometerEvents` with `gyroscopeEvents` or `magnetometerEvents` respectively. Each sensor event provides relevant data, such as x, y, and z values.

## Using Sensor Data in MaterialApp

In a MaterialApp, we can utilize the sensor data for various purposes like controlling the UI elements or updating the screen based on the device's movement. Let's see an example of using the accelerometer sensor to change the background color of the MaterialApp based on the device's tilt:

```dart
import 'package:flutter/material.dart';
import 'package:sensors/sensors.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  Color _backgroundColor = Colors.white;
  
  @override
  void initState() {
    super.initState();
    accelerometerEvents.listen((AccelerometerEvent event) {
      setState(() {
        // Calculate the tilt angle
        double tiltAngle = event.x.abs() + event.y.abs() + event.z.abs();
        
        // Change background color based on tilt
        if (tiltAngle > 1.5) {
          _backgroundColor = Colors.blue;
        } else {
          _backgroundColor = Colors.white;
        }
      });
    });
  }
  
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Container(color: _backgroundColor),
    );
  }
}
```

In this example, we create a StatefulWidget, `_MyAppState`, which registers a listener for accelerometer events in its `initState` method. Whenever a new accelerometer event occurs, the `_backgroundColor` is updated based on the tilt angle calculated from the event's x, y, and z values. The MaterialApp's background color is then set based on the updated `_backgroundColor` value.

## Conclusion

By utilizing the device sensors in a MaterialApp, we can create more interactive and dynamic user interfaces that respond to the device's movements. The `sensors` package provides a convenient way to access and leverage sensor data in Flutter applications.

[#sensors](#sensors) [#flutter](#flutter)