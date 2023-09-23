---
layout: post
title: "Building weather forecasting applications in Flutter WebAssembly"
description: " "
date: 2023-09-24
tags: [Flutter, WebAssembly]
comments: true
share: true
---

Flutter has become a popular choice for developing cross-platform applications, and with the introduction of Flutter WebAssembly, developers can now build applications that run directly in the browser. In this blog post, we will explore how to build a weather forecasting application using Flutter WebAssembly.

## Getting Started with Flutter WebAssembly

To get started, ensure that you have Flutter version 2.5 or above installed on your machine. You can check your Flutter version by running the following command:

```bash
flutter --version
```

If you don't have Flutter installed, you can follow the official Flutter installation guide to install it on your machine.

Next, you need to enable Flutter Web and WebAssembly support. Run the following command to enable it:

```bash
flutter config --enable-web
```

Once enabled, you can create a new Flutter project using the `flutter create` command:

```bash
flutter create my_weather_app
```

Navigate to the project directory:

```bash
cd my_weather_app
```

## Integrating a Weather API

To fetch weather data, we'll integrate a weather API into our application. Various free and paid weather APIs are available, such as OpenWeatherMap, Weatherbit, or AccuWeather. Choose an API that suits your needs and obtain an API key.

Next, we need to add the necessary dependencies to our `pubspec.yaml` file. Open the file and add the following lines:

```yaml
dependencies:
  http: ^0.13.3
```

This will add the HTTP package that we'll use to make API requests. Run the following command to fetch the dependencies:

```bash
flutter pub get
```

## Fetching Weather Data

Create a new file called `weather_service.dart` in the `lib` directory, and add the following code:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

class WeatherService {
  final String baseUrl = 'https://api.weatherapi.com/v1';
  final String apiKey = 'YOUR_API_KEY';

  Future<dynamic> fetchWeatherData(String location) async {
    final Uri uri = Uri.parse('$baseUrl/current.json?key=$apiKey&q=$location');
    final response = await http.get(uri);

    if (response.statusCode == 200) {
      return json.decode(response.body);
    } else {
      throw Exception('Failed to fetch weather data');
    }
  }
}
```

Replace `YOUR_API_KEY` with the actual API key obtained from the weather API provider.

## Building the User Interface

Now, let's create the user interface for our weather forecasting application. Open the `lib/main.dart` file, and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'weather_service.dart';

void main() {
  runApp(MyWeatherApp());
}

class MyWeatherApp extends StatelessWidget {
  final WeatherService weatherService = WeatherService();
  final TextEditingController locationController = TextEditingController();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Weather Forecast'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text(
                'Enter location:',
                style: TextStyle(fontSize: 20.0),
              ),
              SizedBox(height: 16.0),
              Padding(
                padding: EdgeInsets.symmetric(horizontal: 32.0),
                child: TextField(
                  controller: locationController,
                  decoration: InputDecoration(
                    hintText: 'City, Country',
                  ),
                ),
              ),
              SizedBox(height: 16.0),
              ElevatedButton(
                onPressed: () {
                  fetchWeatherData();
                },
                child: Text('Get Weather'),
              ),
            ],
          ),
        ),
      ),
    );
  }

  Future<void> fetchWeatherData() async {
    final String location = locationController.text;
    final dynamic weatherData = await weatherService.fetchWeatherData(location);
    print(weatherData);
    // Process weather data and update UI
  }
}
```

## Running the application

To run the Flutter WebAssembly application, execute the following command:

```bash
flutter run -d chrome
```

The application will launch in a new Chrome window. Enter a location in the text field and click the "Get Weather" button to fetch the weather data from the API.

## Conclusion

In this blog post, we have explored how to build a weather forecasting application using Flutter WebAssembly. We integrated a weather API to fetch the weather data and displayed it on the user interface. Flutter WebAssembly opens up new possibilities for building cross-platform applications that run directly in the browser, reaching a wider range of users. Happy coding!

#Flutter #WebAssembly