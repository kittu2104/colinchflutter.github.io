---
layout: post
title: "Building weather applications with Flutter's weather widget"
description: " "
date: 2023-09-14
tags: [weatherapp]
comments: true
share: true
---

Flutter is a popular cross-platform framework for building beautiful and engaging applications. With its rich set of pre-built widgets, creating weather applications becomes much simpler and efficient. In this blog post, we will discuss how to utilize Flutter's weather widget to build weather applications that display real-time weather information.

## Getting Started with Flutter's Weather Widget
To get started, make sure you have Flutter installed on your system. If not, you can follow the official Flutter installation guide to get it set up. Once Flutter is installed, you can create a new Flutter project using the following command:

```bash
flutter create weather_app
```

After the project is created, navigate to the project directory:

```bash
cd weather_app
```

## Adding Dependencies
Flutter provides various packages and libraries to enhance the development experience. For weather applications, we can include the **weather** package to access weather data from different sources. To include the package, open the `pubspec.yaml` file and add the following line under `dependencies`:

```yaml
dependencies:
  flutter:
    sdk: flutter
    
  weather: ^1.0.0
```

Save the file and run the following command in the project directory to install the new dependency:

```bash
flutter pub get
```

## Creating the Weather Widget
Now, let's create a new Flutter widget to display the weather information. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:weather/weather.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
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
  WeatherFactory _weatherFactory = WeatherFactory("YOUR_API_KEY");

  Weather? _currentWeather;

  @override
  void initState() {
    super.initState();
    _getCurrentWeather();
  }

  void _getCurrentWeather() async {
    Weather? weather = await _weatherFactory.currentWeatherByCityName("New York");
    setState(() {
      _currentWeather = weather;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Weather App'),
      ),
      body: Center(
        child: _currentWeather != null
            ? Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Icon(
                    _currentWeather!.weatherCondition.icon,
                    size: 70,
                  ),
                  SizedBox(height: 20),
                  Text(
                    '${_currentWeather!.temperature.celsius.round()}°C',
                    style: TextStyle(fontSize: 24),
                  ),
                  SizedBox(height: 10),
                  Text(
                    _currentWeather!.areaName,
                    style: TextStyle(fontSize: 18),
                  ),
                ],
              )
            : CircularProgressIndicator(),
      ),
    );
  }
}
```

This code sets up a basic Flutter application with a `WeatherScreen` widget that displays the current weather information. Replace `"YOUR_API_KEY"` with your actual API key obtained from a weather API provider.

## Testing the Application
To test the application, connect a device or use an emulator and run the following command in the project directory:

```bash
flutter run
```

This will launch the weather application on the device or emulator. You should see the application title and a loading indicator initially. Once the weather data is fetched, the application will display the weather icon, temperature, and area name.

## Conclusion
In this blog post, we explored how to leverage Flutter's weather widget to build weather applications. By integrating weather APIs and utilizing the pre-built widgets, Flutter allows developers to create visually appealing and interactive weather apps quickly and easily. Start building your weather application now and provide users with real-time weather updates!

#flutter #weatherapp