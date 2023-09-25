---
layout: post
title: "Creating a responsive weather app using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [weatherapp]
comments: true
share: true
---

![flutter-weather-app](https://example.com/images/flutter-weather-app.jpg)

In this tutorial, we will learn how to create a responsive weather app using `MediaQuery` in Flutter. `MediaQuery` is a powerful Flutter class that allows us to retrieve information about the current device's size and orientation.

## Prerequisites

Before we get started, make sure you have Flutter SDK and a code editor like Visual Studio Code installed on your machine.

## Setup

1. Open your terminal and run the following command to create a new Flutter project:
   ```
   flutter create weather_app
   ```

2. Change directory to the project's folder:
   ```
   cd weather_app
   ```

3. Open the project in your code editor.

## Implementation

1. Open the `lib/main.dart` file and delete the default code.

2. Import the necessary dependencies:
   ```dart
   import 'package:flutter/material.dart';
   ```

3. Create a `WeatherApp` widget:
   ```dart
   void main() {
     runApp(WeatherApp());
   }

   class WeatherApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return MaterialApp(
         title: 'Weather App',
         theme: ThemeData(
           primarySwatch: Colors.blue,
         ),
         home: WeatherHome(),
       );
     }
   }
   ```

4. Create a `WeatherHome` widget as the app's home screen:
   ```dart
   class WeatherHome extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: Text('Weather App'),
         ),
         body: _buildWeatherBody(context),
       );
     }

     Widget _buildWeatherBody(BuildContext context) {
       return Center(
         child: Container(
           width: MediaQuery.of(context).size.width * 0.8,
           height: MediaQuery.of(context).size.height * 0.6,
           color: Colors.blue,
           child: Text(
             'Weather Information',
             style: TextStyle(
               fontSize: 20,
               color: Colors.white,
             ),
           ),
         ),
       );
     }
   }
   ```

5. Run the app on your device or emulator:
   ```
   flutter run
   ```

## Conclusion

In this tutorial, we have learned how to create a responsive weather app using `MediaQuery` in Flutter. By leveraging `MediaQuery`, we can dynamically adjust the UI elements based on the device's size and orientation. This allows our app to provide a great user experience on a wide range of devices.

Feel free to customize the app's UI and integrate real weather data by making API calls. Happy coding!

#flutter #weatherapp