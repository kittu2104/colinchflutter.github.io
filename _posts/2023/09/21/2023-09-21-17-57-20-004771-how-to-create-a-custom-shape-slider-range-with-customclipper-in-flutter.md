---
layout: post
title: "How to create a custom shape slider range with CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: [flutter]
comments: true
share: true
---

Flutter provides a rich set of widgets to build user interfaces. One of the key elements of a great UI is a slider range that allows users to select a range of values. While Flutter offers a default slider widget, it may not always fit the desired design or user experience. In such cases, we can utilize the power of Flutter's `CustomClipper` to create a custom shape slider range. 

## Prerequisites
To follow along with this tutorial, make sure you have Flutter and Dart properly installed on your machine.

## Step 1: Set up a Flutter project
Create a new Flutter project using the following command in your terminal:
```shell
flutter create custom_slider_range
```

Change your working directory to the newly created project:
```shell
cd custom_slider_range
```

## Step 2: Implement the custom shape slider range widget
Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Shape Slider Range',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SliderRangePage(),
    );
  }
}

class SliderRangePage extends StatefulWidget {
  @override
  _SliderRangePageState createState() => _SliderRangePageState();
}

class _SliderRangePageState extends State<SliderRangePage> {
  double _startValue = 0;
  double _endValue = 100;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Shape Slider Range'),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          Slider(
            value: _startValue,
            min: 0,
            max: 100,
            onChanged: (value) {
              setState(() {
                _startValue = value;
              });
            },
          ),
          SizedBox(height: 20),
          Slider(
            value: _endValue,
            min: 0,
            max: 100,
            onChanged: (value) {
              setState(() {
                _endValue = value;
              });
            },
          ),
        ],
      ),
    );
  }
}
```

In the above code, we created a new Flutter project and replaced the default code with a basic app structure. The `SliderRangePage` is a stateful widget that contains two `Slider` widgets - one for the start value and the other for the end value of the range. The `Slider` widget allows users to slide and select the desired values.

## Step 3: Creating a CustomClipper for the slider range
Let's define a `CustomClipper` class that will create the desired custom shape for our slider range. Add the following code to the `lib/main.dart` file:

```dart
class CustomSliderClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    final path = Path();
    path.lineTo(size.width, 0);
    path.lineTo(size.width, size.height * 0.5);
    path.lineTo(0.0, size.height * 0.5);
    path.close();
    return path;
  }

  @override
  bool shouldReclip(CustomSliderClipper oldClipper) => false;
}
```

In the above code, we created a custom `CustomSliderClipper` class that extends `CustomClipper<Path>`. The `getClip()` method defines the shape of our slider range by creating a `Path` object. In this example, we created a rectangular shape that starts from the bottom left corner and ends at the bottom right corner. Feel free to modify the `getClip()` method to create your desired shape.

## Step 4: Applying the custom shape to the slider range
To apply the custom shape to the slider range, we need to wrap the `Slider` widgets with a `ClipPath` widget and provide an instance of our `CustomSliderClipper` class as the `clipper` property. 

```dart
ClipPath(
  clipper: CustomSliderClipper(),
  child: Slider(
    value: _startValue,
    min: 0,
    max: 100,
    onChanged: (value) {
      setState(() {
        _startValue = value;
      });
    },
  ),
),
```

Add this code to replace the first `Slider` widget in the `_SliderRangePageState` class's `build()` method.

Similarly, wrap the second `Slider` widget with a `ClipPath` widget to apply the same custom shape.

```dart
ClipPath(
  clipper: CustomSliderClipper(),
  child: Slider(
    value: _endValue,
    min: 0,
    max: 100,
    onChanged: (value) {
      setState(() {
        _endValue = value;
      });
    },
  ),
),
```

## Step 5: Running the app
Save the changes and run the app using the following command in your terminal:
```shell
flutter run
```

You should now see the custom shape slider range in your running Flutter app. You can slide the start and end values within the range of 0 to 100 and observe the custom shape being applied.

Congratulations! You have successfully created a custom shape slider range with `CustomClipper` in Flutter.

## Conclusion
In this tutorial, we learned how to create a custom shape slider range using `CustomClipper` in Flutter. With the powerful flexibility provided by Flutter's `CustomClipper`, we can create unique and visually appealing sliders for our apps. Feel free to experiment and tweak the code to create different custom shapes for your slider range. Happy coding!

#flutter #UI