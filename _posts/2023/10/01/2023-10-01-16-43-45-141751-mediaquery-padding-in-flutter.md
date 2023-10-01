---
layout: post
title: "MediaQuery padding in Flutter"
description: " "
date: 2023-10-01
tags: [Flutter, MediaQuery, Padding]
comments: true
share: true
---

When building user interfaces in Flutter, it's important to consider different screen sizes and resolutions. Flutter provides a convenient way to handle responsive layouts using `MediaQuery`. One common task is setting different padding values based on the screen size. In this blog post, we will explore how to set padding using `MediaQuery` in Flutter.

## Getting Started

To get started, make sure you have Flutter installed on your machine. You can follow the official Flutter installation guide to set it up. Once you have Flutter installed, create a new Flutter project using the following command:

```bash
flutter create media_query_padding
```

Open the project in your preferred code editor and navigate to the `lib` directory. Open the `main.dart` file and let's dive into setting padding using `MediaQuery`.

## Setting Padding using MediaQuery

`MediaQuery` is a widget that provides the size and orientation of the current device screen. To set padding based on the screen size, we use the `MediaQuery` widget along with the `padding` property.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      body: SafeArea(
        child: Center(
          child: Builder(
            builder: (BuildContext context) {
              // Get the screen size using MediaQuery
              final Size size = MediaQuery.of(context).size;

              // Define padding values based on screen width
              final EdgeInsets padding = size.width > 600
                  ? EdgeInsets.symmetric(horizontal: 50)
                  : EdgeInsets.symmetric(horizontal: 20);

              return Container(
                padding: padding,
                child: Text(
                  'Welcome to MediaQuery Padding',
                  textAlign: TextAlign.center,
                  style: TextStyle(fontSize: 20),
                ),
              );
            },
          ),
        ),
      ),
    ),
  ));
}
```

In this example, we define two sets of padding values based on the screen width. If the screen width is greater than 600, we set a padding of 50 on the horizontal axis; otherwise, we set a padding of 20. You can adjust these values as per your requirements.

## Conclusion

`MediaQuery` is a powerful tool in Flutter for handling responsive layouts. With the help of `MediaQuery`, we can set padding based on the screen size, providing a better user experience across different devices. By leveraging the `MediaQuery` widget, you can make your apps easily adapt to varying screen sizes, ultimately improving the usability and aesthetics of your Flutter applications.

Remember to import the necessary libraries and wrap your widgets with the appropriate containers and scaffolds. By using `MediaQuery` padding, you can ensure your app looks great on different devices without compromising on usability.

#Flutter #MediaQuery #Padding