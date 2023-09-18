---
layout: post
title: "Building a custom music player UI with Flutter Custom Painter"
description: " "
date: 2023-09-15
tags: [customui]
comments: true
share: true
---

Are you looking to create a unique and custom music player UI for your Flutter app? Look no further! In this tutorial, we will explore how to use **Flutter Custom Painter** to design and implement a beautiful music player user interface. So, let's get started!

## What is Flutter Custom Painter?

**Flutter Custom Painter** is a powerful widget that allows you to create custom graphics and animations by providing a **Canvas** to draw on. This gives you the flexibility to design and draw complex UI elements according to your requirements. In our case, we will be using it to create a custom music player UI.

## Creating the Music Player UI

To begin, let's create a new Flutter project and open the main.dart file. We will start by importing the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/painting.dart';
```

Next, we will define our custom music player UI widget by extending the **CustomPainter** class. Inside this widget, we will override the **paint()** and **shouldRepaint()** methods:

```dart
class MusicPlayerPainter extends CustomPainter {
  @override
  void paint(Canvas canvas, Size size) {
    // Define your custom UI elements here
  }

  @override
  bool shouldRepaint(MusicPlayerPainter oldDelegate) => false;
}
```

Within the **paint()** method, you can use various **Canvas** functions to draw different elements like rectangles, circles, lines, and more on the canvas.

Now, let's utilize the custom painter widget in our main app. Replace the existing **MyApp** class with the following code:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Music Player',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: Scaffold(
        appBar: AppBar(title: Text('Custom Music Player')),
        body: CustomPaint(painter: MusicPlayerPainter()),
      ),
    );
  }
}
```

In this code, we are wrapping our **CustomPaint** widget inside the **body** of a **Scaffold**, which provides a basic app structure with an app bar.

## Drawing the Custom UI Elements

Now that we have set up our custom painter, we can start drawing the different UI elements of our music player. Here are some examples:

### Drawing buttons

```dart
canvas.drawRRect(
  RRect.fromRectAndRadius(
    Rect.fromCenter(
      center: Offset(size.width * 0.5, size.height * 0.8),
      width: 80,
      height: 40,
    ),
    Radius.circular(20),
  ),
  Paint()..color = Colors.blue,
);
```

### Drawing progress bar

```dart
canvas.drawRect(
  Rect.fromLTWH(
    size.width * 0.1,
    size.height * 0.6,
    size.width * 0.8,
    8,
  ),
  Paint()..color = Colors.grey[300],
);

canvas.drawRect(
  Rect.fromLTWH(
    size.width * 0.1,
    size.height * 0.6,
    size.width * 0.5,
    8,
  ),
  Paint()..color = Colors.blue,
);
```

### Drawing album art

```dart
canvas.drawCircle(
  Offset(size.width * 0.5, size.height * 0.3),
  100,
  Paint()..color = Colors.grey[300],
);

canvas.drawCircle(
  Offset(size.width * 0.5, size.height * 0.3),
  90,
  Paint()..color = Colors.white,
);

// Draw the album image here
```

These are just a few examples of what you can achieve with Flutter Custom Painter. Play around with different shapes, sizes, and colors to create your own unique music player UI.

## Conclusion

In this tutorial, we learned how to create a custom music player UI using **Flutter Custom Painter**. We explored the basics of the **CustomPainter** class, drawing different UI elements, and incorporating the custom painter into our Flutter app. With this knowledge, you can now create amazing and customize user interfaces for your music player app.

So why wait? Start designing and building your own custom music player UI with Flutter Custom Painter today! 

#flutter #customui