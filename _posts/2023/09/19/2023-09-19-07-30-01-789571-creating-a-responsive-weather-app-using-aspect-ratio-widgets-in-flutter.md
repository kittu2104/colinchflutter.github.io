---
layout: post
title: "Creating a responsive weather app using Aspect Ratio widgets in Flutter"
description: " "
date: 2023-09-19
tags: [Flutter, WeatherApp]
comments: true
share: true
---

Flutter is a popular cross-platform framework for building beautiful and responsive mobile applications. In this tutorial, we will explore how to create a responsive weather app using Aspect Ratio widgets in Flutter, allowing our app to adjust its layout based on different screen sizes and orientations.

## Getting Started

Before we dive into the code, make sure you have Flutter installed on your machine. You can download Flutter from the official website and follow the installation instructions.

Once Flutter is installed, create a new Flutter project and open it in your favorite code editor.

## Adding Weather API

To display weather data in our app, we need to connect it to a weather API. There are several weather APIs available, such as OpenWeatherMap and Weatherbit. You can choose whichever API suits your needs.

Follow the documentation of your chosen weather API to make API requests and retrieve weather data based on the user's location or any predefined location.

## Designing the UI

Next, let's design the user interface of our weather app. We will use AspectRatio widgets to ensure our layout maintains the proper aspect ratio on different screen sizes.

First, create a new file named `weather_screen.dart` and add the following code:

```dart
import 'package:flutter/material.dart';

class WeatherScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Weather App'),
      ),
      body: SafeArea(
        child: AspectRatio(
          aspectRatio: 16 / 9, // Set the desired aspect ratio
          child: Container(
            // Add weather widgets here
          ),
        ),
      ),
    );
  }
}
```

In this code snippet, we create a `WeatherScreen` widget that extends the `StatelessWidget` class. We use the `AspectRatio` widget as the root widget of our screen, specifying the desired aspect ratio for our weather interface.

## Displaying Weather Widgets

Inside the `Container` widget, we can now add the individual weather widgets based on our weather API response.

For example, let's add a `Column` widget to display the weather details vertically. Modify the `Container` widget in the previous code snippet as follows:

```dart
Container(
  decoration: BoxDecoration(
    gradient: LinearGradient(
      colors: [Colors.blue, Colors.white],
      begin: Alignment.topCenter,
      end: Alignment.bottomCenter,
    ),
  ),
  child: Column(
    children: [
      Text(
        'City Name',
        style: TextStyle(
          fontSize: 24,
          fontWeight: FontWeight.bold,
          color: Colors.white,
        ),
      ),
      Text(
        'Temperature: 25°C',
        style: TextStyle(
          fontSize: 18,
          color: Colors.white,
        ),
      ),
      // Add more weather details here
    ],
  ),
),
```

In this updated code snippet, we wrap the `Container` widget with a gradient background using the `LinearGradient` widget for a visually appealing look. Inside the `Column` widget, we add `Text` widgets to display the city name and temperature.

## Running the App

To see our responsive weather app in action, we need to add the `WeatherScreen` as the entry point of our app.

Open the `main.dart` file, remove the default code, and replace it with the following:

```dart
import 'package:flutter/material.dart';
import 'weather_screen.dart';

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
```

Now, run the app using the `flutter run` command, and you should see the weather interface with the defined aspect ratio on your device.

## Conclusion

In this tutorial, we learned how to create a responsive weather app using Aspect Ratio widgets in Flutter. We explored the basics of UI design and utilized AspectRatio widgets to maintain the proper layout on different screen sizes.

Remember to adapt the code to your specific weather API and add more weather details as needed. With Flutter's flexibility, you can further enhance and customize your weather app to deliver a delightful user experience.

#Flutter #WeatherApp