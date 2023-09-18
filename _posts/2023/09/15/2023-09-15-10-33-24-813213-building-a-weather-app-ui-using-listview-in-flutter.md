---
layout: post
title: "Building a weather app UI using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [WeatherApp]
comments: true
share: true
---

Flutter is a powerful framework for building beautiful and interactive user interfaces. In this tutorial, we will learn how to build a weather app UI using the `ListView` widget in Flutter.

## Prerequisites
Before we begin, make sure you have Flutter and Dart installed on your machine. If you haven't installed them yet, please refer to the official Flutter documentation for installation instructions.

## Setting up the project
To get started, open your preferred code editor and create a new Flutter project. You can do this by running the following command in your terminal:

```dart
flutter create weather_app
```

## Adding dependencies
Next, we need to add some dependencies to our `pubspec.yaml` file. Open the `pubspec.yaml` file and add the following lines under the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.0
  cached_network_image: ^3.0.0
```

Save the file, and run the following command in your terminal to fetch the newly added dependencies:

```dart
flutter pub get
```

## Creating the weather widget
In Flutter, we can create a weather widget that displays the weather information for a particular location. We will use the `ListView` widget to create a scrolling list of weather widgets.

To create the weather widget, open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

class WeatherWidget extends StatelessWidget {
  final String location;
  final String temperature;

  WeatherWidget({required this.location, required this.temperature});

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.all(16.0),
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          Text(
            location,
            style: TextStyle(
              fontWeight: FontWeight.bold,
              fontSize: 18.0,
            ),
          ),
          SizedBox(height: 8.0),
          Text(
            temperature,
            style: TextStyle(
              fontSize: 24.0,
            ),
          ),
        ],
      ),
    );
  }
}
```

The `WeatherWidget` class takes in two required parameters: `location` and `temperature`. It uses a `Container` widget to provide padding and a `Column` widget to arrange the text components vertically.

## Building the weather app UI
Now that we have created the weather widget, let's build the UI for our weather app. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:cached_network_image/cached_network_image.dart';
import 'package:http/http.dart' as http;
import 'dart:convert';

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
      home: WeatherScreen(),
    );
  }
}

class WeatherScreen extends StatefulWidget {
  @override
  _WeatherScreenState createState() => _WeatherScreenState();
}

class _WeatherScreenState extends State<WeatherScreen> {
  List<Weather> weatherData = [];

  @override
  void initState() {
    super.initState();
    fetchWeatherData();
  }

  Future<void> fetchWeatherData() async {
    final response = await http.get(Uri.parse('https://api.example.com/weather'));

    if (response.statusCode == 200) {
      final data = jsonDecode(response.body);
      final List<Weather> weatherList = [];

      for (var item in data['weather']) {
        final location = item['location'];
        final temperature = item['temperature'];

        weatherList.add(
          Weather(location: location, temperature: temperature),
        );
      }

      setState(() {
        weatherData = weatherList;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Weather App'),
      ),
      body: ListView.builder(
        itemCount: weatherData.length,
        itemBuilder: (context, index) {
          return WeatherWidget(
            location: weatherData[index].location,
            temperature: weatherData[index].temperature,
          );
        },
      ),
    );
  }
}

class Weather {
  final String location;
  final String temperature;

  Weather({required this.location, required this.temperature});
}
```

In this code, we have defined a `WeatherScreen` widget as the home screen of our app. Inside the `WeatherScreen` widget, we use the `ListView.builder` widget to create a list of `WeatherWidget` instances based on the data fetched from an API.

We provide the `location` and `temperature` values to each `WeatherWidget` based on the weather data received from the API.

## Running the app
To run the app, connect a device or emulator and execute the following command in your terminal:

```dart
flutter run
```

Congratulations! You have successfully built a weather app UI using `ListView` in Flutter.

## #Flutter #WeatherApp