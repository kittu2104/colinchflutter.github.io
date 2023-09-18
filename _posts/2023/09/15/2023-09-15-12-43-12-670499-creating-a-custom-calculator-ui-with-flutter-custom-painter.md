---
layout: post
title: "Creating a custom calculator UI with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [custompainter]
comments: true
share: true
---

Flutter is a powerful cross-platform development framework that allows you to build beautiful user interfaces. In this tutorial, we will explore how to create a custom calculator UI using Flutter Custom Painter.

## What is Flutter Custom Painter?

**Flutter Custom Painter** is a powerful widget that allows you to create your own custom drawings on the canvas. It provides a low-level API that gives you full control over the pixel-level details of the drawing process.

## Getting Started

Before we dive into creating the custom calculator UI, make sure you have Flutter installed on your system. If you don't, you can follow the official Flutter documentation to set it up.

## Creating the Custom Calculator UI

Let's start by creating a new Flutter project and setting up the necessary dependencies. Open your preferred terminal and execute the following commands:

```bash
flutter create custom_calculator
cd custom_calculator
```

Next, open the `lib/main.dart` file in your favorite code editor and remove the existing code. Replace it with the following code:

```dart
import 'package:flutter/material.dart';

void main() => runApp(CustomCalculatorApp());

class CustomCalculatorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Calculator',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CustomCalculatorScreen(),
    );
  }
}

class CustomCalculatorScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Calculator'),
      ),
      body: Center(
        child: Text(
          'Calculator UI',
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

Save the changes and run the app using the following command:

```bash
flutter run
```

You should now see a basic app with the title "Custom Calculator" and a centered text widget saying "Calculator UI".

## Creating the Calculator UI Custom Painter

To draw the calculator UI, we will create a new class `CalculatorPainter` that extends `CustomPainter`. This class will be responsible for the custom drawing logic of our calculator. Replace the contents of your `lib/main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';

void main() => runApp(CustomCalculatorApp());

class CustomCalculatorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Calculator',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CustomCalculatorScreen(),
    );
  }
}

class CustomCalculatorScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Calculator'),
      ),
      body: CustomPaint(
        painter: CalculatorPainter(),
        child: Container(),
      ),
    );
  }
}

class CalculatorPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // TODO: Add custom drawing logic here
  }

  @override
  bool shouldRepaint(CalculatorPainter oldDelegate) {
    return false;
  }
}
```

In the code above, we have added a `CustomPaint` widget to the `body` of our `CustomCalculatorScreen`. The `CustomPaint` widget takes a `painter` argument, which is an instance of our `CalculatorPainter` class.

In the `CalculatorPainter` class, the `paint` method is responsible for custom drawing logic. We'll add the necessary code there in the next steps.

## Drawing the Calculator Buttons

To draw the calculator buttons, we'll utilize the `drawRect()` method provided by the `Canvas` class. Update the `paint` method in the `CalculatorPainter` class with the following code:

```dart
class CalculatorPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    final buttonWidth = size.width / 4;
    final buttonHeight = size.height / 6;

    final paint = Paint();
    paint.color = Colors.grey;
    paint.style = PaintingStyle.fill;

    final buttonRect = Rect.fromLTWH(0, 0, buttonWidth, buttonHeight);
    canvas.drawRect(buttonRect, paint);
  }

  @override
  bool shouldRepaint(CalculatorPainter oldDelegate) {
    return false;
  }
}
```

In the code above, we define the `buttonWidth` and `buttonHeight` variables to calculate the dimensions of each button based on the size of the `CustomPaint` widget.

We then create a `Paint` object and set its color to grey and style to fill. Next, we define a `buttonRect` using the `Rect.fromLTWH()` method, which represents the position and dimensions of the button. Finally, we use the `canvas.drawRect()` method to draw the button on the canvas.

Save the changes and run the app using `flutter run`. You should now see a grey rectangle drawn on the canvas, representing the first calculator button.

## Conclusion

In this tutorial, we explored how to create a custom calculator UI using Flutter Custom Painter. We learned about the basics of Flutter Custom Painter, created a custom drawing class, and added custom drawing logic to draw the calculator buttons.

Feel free to experiment further and customize the layout and appearance of the calculator UI according to your needs. Happy coding! 🚀

## #flutter #custompainter