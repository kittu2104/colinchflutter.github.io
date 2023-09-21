---
layout: post
title: "How to create a custom shape slider with CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [flutter, customshapeslider]
comments: true
share: true
---

In Flutter, you can create custom shapes for various UI elements, including sliders. One way to achieve this is by using the `CustomClipper` class. In this tutorial, we will guide you through the process of creating a custom shape slider with `CustomClipper` in Flutter.

## Step 1: Set up a new Flutter project

First, make sure you have Flutter installed on your machine. Create a new Flutter project by running the following command in your terminal:

```dart
flutter create custom_shape_slider
```

Change to the project directory:

```dart
cd custom_shape_slider
```

## Step 2: Add dependencies

Next, open the `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  animated_text_kit: ^4.2.1
```

Save the file and run the following command to fetch the dependencies:

```dart
flutter packages get
```

## Step 3: Create a CustomShapeSlider class

Now, let's create a new file named `custom_shape_slider.dart` inside the `lib` directory. Add the following code to define the `CustomShapeSlider` class:

```dart
import 'package:flutter/material.dart';

class CustomShapeSlider extends StatefulWidget {
  @override
  _CustomShapeSliderState createState() => _CustomShapeSliderState();
}

class _CustomShapeSliderState extends State<CustomShapeSlider> {
  double _value = 0.0;

  @override
  Widget build(BuildContext context) {
    return Slider(
      value: _value,
      min: 0.0,
      max: 100.0,
      onChanged: (newValue) {
        setState(() {
          _value = newValue;
        });
      },
      activeColor: Colors.blue,
      inactiveColor: Colors.grey,
    );
  }
}
```

In this code, we define a stateful widget `CustomShapeSlider` that extends `StatefulWidget`. Inside the state class `_CustomShapeSliderState`, we declare a `_value` variable to track the slider's current value. The `build` method returns a `Slider` widget with the `_value` variable as its value.

## Step 4: Create a custom shape with CustomClipper

To create a custom shape for the slider thumb, we need to create a class that extends `CustomClipper<Path>`. Let's create a new file named `custom_clipper.dart` inside the `lib` directory and add the following code:

```dart
import 'package:flutter/material.dart';

class CustomSliderThumbShape extends SliderComponentShape {
  final double thumbRadius;
  final double thumbHeight;

  CustomSliderThumbShape({
    this.thumbRadius = 10.0,
    this.thumbHeight = 30.0,
  });

  @override
  Size getPreferredSize(bool isEnabled, bool isDiscrete) {
    return Size.fromRadius(thumbRadius);
  }

  @override
  void paint(
    PaintingContext context,
    Offset center, {
    Animation<double> activationAnimation,
    Animation<double> enableAnimation,
    bool isEnabled,
    bool isDiscrete,
    TextPainter labelPainter,
    RenderBox parentBox,
    SliderThemeData sliderTheme,
    TextDirection textDirection,
    double value,
    double textScaleFactor,
    Size sizeWithOverflow,
  }) {
    final Canvas canvas = context.canvas;
    final sweepAngle = 90.0 * value / sliderTheme.maxValue;

    canvas.drawArc(
      Rect.fromCenter(
        center: center,
        width: thumbRadius * 2,
        height: thumbHeight,
      ),
      -sweepAngle,
      sweepAngle * 2,
      true,
      Paint()..color = sliderTheme.activeTrackColor,
    );
  }
}
```

In this code, we define a class `CustomSliderThumbShape` that extends `SliderComponentShape`. Inside the `paint` method, we use the `Canvas` class to draw a custom shape for the thumb. We calculate the `sweepAngle` based on the slider's current value and draw an arc using the `drawArc` method.

## Step 5: Implement the custom shape slider

To use the custom shape slider in your application, open the `main.dart` file and replace the existing code with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:custom_shape_slider/custom_shape_slider.dart';
import 'package:custom_shape_slider/custom_clipper.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Shape Slider',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom Shape Slider'),
        ),
        body: Center(
          child: CustomShapeSlider(
            thumbShape: CustomSliderThumbShape(
              thumbRadius: 10,
              thumbHeight: 30,
            ),
          ),
        ),
      ),
    );
  }
}
```

In this code, we import the `CustomShapeSlider` widget and the `CustomSliderThumbShape` class. We then use the `CustomShapeSlider` widget as the child of the `Center` widget in the `Scaffold` body. We also set the `thumbShape` property of the `CustomShapeSlider` widget to use the custom thumb shape we defined.

## Step 6: Run the app

Finally, run the app using `flutter run` command in your terminal. You should now see a custom shape slider with a rounded thumb in your application.

Congratulations! You have successfully created a custom shape slider with `CustomClipper` in Flutter. Feel free to customize the custom thumb shape and experiment with different designs according to your requirements.

## Conclusion

In this tutorial, we learned how to create a custom shape slider using `CustomClipper` in Flutter. By defining a custom shape class that extends `SliderComponentShape`, we were able to create a unique thumb shape for the slider. This custom shape slider provides more freedom to design sliders that match your app's style and branding.

#flutter #customshapeslider