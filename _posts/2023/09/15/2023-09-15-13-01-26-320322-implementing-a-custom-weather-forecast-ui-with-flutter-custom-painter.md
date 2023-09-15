---
layout: post
title: "Implementing a custom weather forecast UI with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [flutter, custompainter]
comments: true
share: true
---

![Flutter](https://images.unsplash.com/photo-1611624249883-93f5c3b7511c)

Flutter is a popular open-source UI toolkit for building cross-platform applications. With its powerful and flexible framework, you can create beautiful and customized user interfaces. In this tutorial, we'll explore how to create a custom weather forecast UI using Flutter's Custom Painter.

## Getting Started

To get started, make sure you have Flutter installed on your system. If not, follow the official [Flutter installation guide](https://flutter.dev/docs/get-started/install) to set up Flutter on your machine.

Once Flutter is installed, create a new Flutter project using the following command in your terminal:

```bash
flutter create weather_forecast_ui
```

Navigate to the newly created project directory:

```bash
cd weather_forecast_ui
```

Open the project in your preferred IDE or code editor.

## Adding Dependencies

To use custom painter, we need to add the following dependencies to the `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter

  weather_icons: ^2.0.0
  # Add other dependencies if required
```

Save the file and run the following command to fetch the dependencies:

```bash
flutter pub get
```

## Creating the Custom Weather Forecast UI 

In the `lib` directory, create a new file called `weather_forecast_ui.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:weather_icons/weather_icons.dart';

class WeatherForecastUI extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Weather Forecast'),
      ),
      body: CustomPaint(
        painter: WeatherForecastPainter(),
        child: Container(),
      ),
    );
  }
}

class WeatherForecastPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Implement custom painting logic here
  }

  @override
  bool shouldRepaint(WeatherForecastPainter oldDelegate) {
    return false;
  }
}
```

In the example code above, we create a `WeatherForecastUI` widget that represents the weather forecast screen. Inside the build method, we scaffold the UI with an `AppBar` and a `CustomPaint` widget.

We also create a `WeatherForecastPainter` class that extends `CustomPainter`. This class will handle all the custom painting logic. For now, the `paint` method is empty, and the `shouldRepaint` method returns `false` indicating that the painting does not need to be updated.

## Adding Weather Data

To display the weather forecast, we need to fetch weather data and paint it on the UI. You can use any weather API to retrieve the data. For simplicity, let's assume we have a list of weather data available as `List<WeatherData>`.

In the `WeatherForecastPainter` class, add a property to hold the weather data and modify the `paint` method as follows:

```dart
class WeatherForecastPainter extends CustomPainter {
  final List<WeatherData> weatherData;

  WeatherForecastPainter(this.weatherData);

  @override
  void paint(Canvas canvas, Size size) {
    // Implement custom painting logic here
    // Use weatherData to draw weather forecast details
  }
  
  // ...
}
```

## Drawing the Weather Forecast

To draw the weather forecast, we can use various shapes, icons, and colors provided by Flutter. Modify the `paint` method in the `WeatherForecastPainter` class to add the necessary painting logic:

```dart
class WeatherForecastPainter extends CustomPainter {
  // ...

  @override
  void paint(Canvas canvas, Size size) {
    final center = Offset(size.width / 2, size.height / 2);
    final radius = size.width / 2 - 20;
    final strokeWidth = 5.0;

    final paint = Paint()
      ..color = Colors.blue
      ..strokeWidth = strokeWidth
      ..style = PaintingStyle.stroke;

    canvas.drawCircle(center, radius, paint);

    final textPainter = TextPainter(
      text: TextSpan(
        text: 'Weather Forecast',
        style: TextStyle(fontSize: 20, color: Colors.black),
      ),
      textAlign: TextAlign.center,
      textDirection: TextDirection.ltr,
    );
    textPainter.layout(minWidth: 0, maxWidth: size.width);
    textPainter.paint(canvas, center - Offset(textPainter.width / 2, textPainter.height / 2));

    // Draw weather forecast details using weatherData
    for (final data in weatherData) {
      // Draw weather icons, temperature, etc.
    }
  }

  // ...
}
```

In the example code above, we begin by drawing a circle using canvas's `drawCircle` method to represent the overall weather forecast area. We also add a text painter to display the title of the UI.

Next, we iterate through the `weatherData` list and draw weather icons, temperature, and other forecast details using appropriate methods and widgets.

## Putting It All Together

Finally, let's integrate our custom weather forecast UI into the main app. In the `main.dart` file, replace the default `MyApp` widget with the `WeatherForecastUI` widget:

```dart
import 'package:flutter/material.dart';
import 'package:weather_forecast_ui/weather_forecast_ui.dart';

void main() {
  runApp(WeatherForecastApp());
}

class WeatherForecastApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Weather Forecast App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: WeatherForecastUI(),
    );
  }
}
```

Save the file and run the app using the following command:

```bash
flutter run
```

Now you should see the initial custom weather forecast UI with a circular area and a title.

## Conclusion

In this tutorial, we learned how to implement a custom weather forecast UI using Flutter's Custom Painter. We explored the basics of styling and rendering using the `CustomPaint` widget and wrote a custom `WeatherForecastPainter` class to handle the painting logic. By extending this example, you can create more detailed and interactive weather forecast UIs with Flutter.

#flutter #custompainter