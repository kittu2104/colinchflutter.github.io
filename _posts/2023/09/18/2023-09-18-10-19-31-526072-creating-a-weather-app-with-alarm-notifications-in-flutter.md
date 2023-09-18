---
layout: post
title: "Creating a weather app with alarm notifications in Flutter"
description: " "
date: 2023-09-18
tags: [weatherapp]
comments: true
share: true
---

In today's blog post, we will explore how to create a weather app with alarm notifications using Flutter. This app will not only provide real-time weather information but also allow users to set alarms based on weather conditions. Let's get started!

## Setting up the Project

First, make sure you have Flutter installed on your system. If not, refer to the official Flutter documentation for installation instructions.

Once Flutter is set up, create a new Flutter project by running the following command:

```
flutter create weather_app
```

Navigate to the project directory:

```
cd weather_app
```

## Designing the User Interface

Let's start by designing the user interface for our weather app. Open the main.dart file and replace the boilerplate code with the following:

```dart
import 'package:flutter/material.dart';

void main() => runApp(WeatherApp());

class WeatherApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Weather App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: WeatherPage(),
    );
  }
}

class WeatherPage extends StatefulWidget {
  @override
  _WeatherPageState createState() => _WeatherPageState();
}

class _WeatherPageState extends State<WeatherPage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Weather App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Welcome to Weather App',
              style: TextStyle(
                fontSize: 24,
                fontWeight: FontWeight.bold,
              ),
            ),
            SizedBox(height: 16),
            // Add more widgets for weather information and alarm settings
          ],
        ),
      ),
    );
  }
}
```

In the above code, we have set up a basic Flutter app with a title and a scaffold with an app bar. Feel free to customize the UI to fit your requirements.

## Integrating Weather API

To retrieve real-time weather data, we will use a weather API. There are several weather APIs available; for this tutorial, we will use the OpenWeatherMap API.

First, sign up on the OpenWeatherMap website to obtain an API key.

Next, add the http package dependency to your pubspec.yaml file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.4
```

Run `flutter pub get` to fetch the new dependency.

Now, let's make an API request to get weather data. Modify the `_WeatherPageState` class as follows:

```dart
import 'package:http/http.dart' as http;

// ...

class _WeatherPageState extends State<WeatherPage> {
  final String apiKey = 'YOUR_API_KEY';
  final String apiUrl = 'https://api.openweathermap.org/data/2.5/weather?q={city}&appid={apiKey}';

  Future<void> fetchWeatherData() async {
    final response = await http.get(Uri.parse(apiUrl));
    
    if (response.statusCode == 200) {
      // Handle successful API response here
    } else {
      // Handle API error
    }
  }

  @override
  void initState() {
    fetchWeatherData();
    super.initState();
  }

  // ...
}
```

Replace `YOUR_API_KEY` with the API key obtained from OpenWeatherMap. Ensure the `apiUrl` has the city parameter `{city}` and API key parameter `{apiKey}`.

Now, you can parse the API response to retrieve the required weather information and update the UI accordingly.

## Setting Up Alarm Notifications

To set up alarm notifications based on weather conditions, we will utilize the `flutter_local_notifications` package. Add it as a dependency in your pubspec.yaml file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.4
  flutter_local_notifications: ^7.0.0
```

Run `flutter pub get` to fetch the new dependency.

Once the package is added, you can use it to schedule and display alarm notifications based on user settings and weather conditions.

## Conclusion

In this tutorial, we explored how to create a weather app with alarm notifications using Flutter. We covered setting up the project, designing the UI, integrating a weather API, and setting up alarm notifications. Feel free to customize the app further and add additional features such as location-based weather data or personalization options.

Stay tuned for more exciting Flutter tutorials. Happy coding!

#flutter #weatherapp