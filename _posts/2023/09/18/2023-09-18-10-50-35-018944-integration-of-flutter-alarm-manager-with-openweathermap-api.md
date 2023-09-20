---
layout: post
title: "Integration of Flutter Alarm Manager with OpenWeatherMap API"
description: " "
date: 2023-09-18
tags: [alarmmanager]
comments: true
share: true
---

In this tutorial, we will learn how to integrate Flutter Alarm Manager with the OpenWeatherMap API to create a weather alarm application. This application will use the Alarm Manager plugin to schedule alarms based on weather conditions retrieved from the OpenWeatherMap API.

## Getting Started

Before we begin, make sure you have Flutter and Dart installed on your machine. 

### Step 1: Setup

Create a new Flutter project using the Flutter CLI or your preferred IDE.

```dart
flutter create weather_alarm
cd weather_alarm
```

### Step 2: Add Flutter Alarm Manager Plugin

Open the `pubspec.yaml` file and add the `flutter_alarm_manager` plugin as a dependency.

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_alarm_manager: ^0.8.1
```

Save the file and run `flutter pub get` to install the package.

### Step 3: Add OpenWeatherMap API Dependency

Next, we need to add the `http` package to make HTTP requests to the OpenWeatherMap API.

```yaml
dependencies:
  http: ^0.13.3
```

### Step 4: Fetch Weather Data

Create a new Dart file called `weather_api.dart`. Inside this file, import the necessary packages.

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
```

Define a function to fetch the weather data from the OpenWeatherMap API.

```dart
Future<Map<String, dynamic>> fetchWeather() async {
  String apiUrl = 'https://api.openweathermap.org/data/2.5/weather?q={CITY_NAME}&appid={API_KEY}';

  final response = await http.get(Uri.parse(apiUrl));
  if (response.statusCode == 200) {
    return json.decode(response.body);
  } else {
    throw Exception('Failed to fetch weather data');
  }
}
```

Replace `{CITY_NAME}` with the desired city name and `{API_KEY}` with your OpenWeatherMap API key.

### Step 5: Schedule Alarms

Import the necessary packages in the main Dart file.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';
```

Inside the `main` function, schedule your alarms based on weather conditions.

```dart
void main() {
  WidgetsFlutterBinding.ensureInitialized();
  AlarmManager.initialize();

  AlarmManager.oneShotAt(DateTime.now().add(Duration(minutes: 5)), 1,
      () => checkWeatherAndSetAlarm());

  runApp(MyApp());
}

void checkWeatherAndSetAlarm() async {
  final weatherData = await fetchWeather();
  final weatherCondition = weatherData['weather'][0]['description'];

  if (weatherCondition.contains('rain')) {
    // Set alarm for rainy weather
    // TODO: Implement alarm logic
  } else if (weatherCondition.contains('snow')) {
    // Set alarm for snowy weather
    // TODO: Implement alarm logic
  } else {
    // Set alarm for other weather conditions
    // TODO: Implement alarm logic
  }
}
```

This code will schedule an alarm to trigger the `checkWeatherAndSetAlarm` function 5 minutes from the current time. Inside this function, we fetch the weather data from the OpenWeatherMap API and check the weather condition. Depending on the condition, you can implement your own logic to set the appropriate alarm.

### Step 6: Build and Run

Run the application using `flutter run` and test the weather alarm functionality. Make sure to grant the necessary permissions for the app to schedule alarms.

## Conclusion

In this tutorial, we learned how to integrate Flutter Alarm Manager with the OpenWeatherMap API to create a weather alarm application. We explored how to fetch weather data and schedule alarms based on weather conditions. Now, you can enhance the app by implementing alarm logic based on different weather conditions.

#flutter #alarmmanager