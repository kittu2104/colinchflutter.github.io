---
layout: post
title: "Designing different layouts for different screen sizes using `MediaQuery`"
description: " "
date: 2023-09-23
tags: [Flutter, Responsivedesign]
comments: true
share: true
---

In today's digital landscape, it's crucial to ensure that your website or application is not only visually appealing but also functional across various devices and screen sizes. With the rise in mobile usage, it's essential to adopt a responsive design approach that allows your content to adapt seamlessly across different devices.

One way to achieve this is by using the `MediaQuery` widget in Flutter, a popular open-source UI toolkit for building natively compiled applications. `MediaQuery` enables you to create different layouts and design elements based on the screen size and orientation of the device.

Let's dive into some code examples to understand how to use `MediaQuery` effectively.

## 1. Responsive Layout

When designing for different screen sizes, the first step is to create a responsive layout that automatically adjusts based on the available screen space. Here's an example of how you can implement a responsive layout using `MediaQuery` in Flutter:

```dart
import 'package:flutter/material.dart';

class ResponsiveLayoutExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Container(
          width: MediaQuery.of(context).size.width * 0.8,
          height: MediaQuery.of(context).size.height * 0.5,
          color: Colors.blue,
          child: Text(
            'Responsive Layout',
            style: TextStyle(fontSize: 20, color: Colors.white),
          ),
        ),
      ),
    );
  }
}
```

In this example, the width and height of the container are set based on the screen size using `MediaQuery`. By multiplying the screen width and height with 0.8 and 0.5, respectively, we ensure that the container occupies 80% of the width and 50% of the height of the device.

## 2. Adaptive Design

Apart from adjusting the layout, `MediaQuery` allows you to make design decisions based on specific screen sizes. For example, you might want to display a different UI for smartphones, tablets, and desktops. Here's an example of how to implement adaptive design using `MediaQuery` in Flutter:

```dart
import 'package:flutter/material.dart';

class AdaptiveDesignExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;

    if (screenWidth > 600) {
      // Tablet or desktop UI
      return Scaffold(
        body: Center(
          child: Container(
            width: 400,
            height: 300,
            color: Colors.blue,
            child: Text(
              'Tablet or Desktop UI',
              style: TextStyle(fontSize: 20, color: Colors.white),
            ),
          ),
        ),
      );
    }

    // Smartphone UI
    return Scaffold(
      body: Center(
        child: Container(
          width: 200,
          height: 150,
          color: Colors.blue,
          child: Text(
            'Smartphone UI',
            style: TextStyle(fontSize: 20, color: Colors.white),
          ),
        ),
      ),
    );
  }
}
```

In this example, we determine the screen width using `MediaQuery` and conditionally render different UI components based on the screen size. If the screen width is greater than 600 pixels, we display a tablet or desktop UI, and for smaller screen sizes, we show a smartphone UI.

By using `MediaQuery` effectively, you can create highly adaptive and responsive designs for your Flutter applications. This ensures that your content looks great and functions well on devices of all sizes, providing a seamless user experience.

Remember, adopting a responsive design approach is key in today's mobile-driven world, and `MediaQuery` is a powerful tool to achieve that.

#Flutter #Responsivedesign