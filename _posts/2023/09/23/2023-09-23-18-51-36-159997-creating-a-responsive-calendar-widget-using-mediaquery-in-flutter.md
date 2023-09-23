---
layout: post
title: "Creating a responsive calendar widget using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [FlutterDev, MobileAppDevelopment]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive calendar widget using `MediaQuery` in Flutter. By using `MediaQuery`, we can make our calendar widget adapt its size and layout based on the screen size of the device.

## Prerequisites
Before we begin, make sure you have Flutter installed on your machine. If not, follow the instructions in the [official Flutter documentation](https://flutter.dev/docs/get-started/install) to get started.

## Setting up the project
Let's start by creating a new Flutter project. Open your terminal or command prompt and run the following command:

```
flutter create responsive_calendar
```

Once the project is created, navigate into the project directory:

```
cd responsive_calendar
```

Now open the `lib/main.dart` file and remove the existing code. Replace it with the following code:

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Calendar',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: CalendarPage(),
    );
  }
}

class CalendarPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final MediaQueryData mediaQuery = MediaQuery.of(context);
    final double deviceWidth = mediaQuery.size.width;
    final double deviceHeight = mediaQuery.size.height;

    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Calendar'),
      ),
      body: Container(
        width: deviceWidth * 0.8,
        height: deviceHeight * 0.6,
        child: Text('Calendar Widget'),
      ),
    );
  }
}
```

In the code above, we use the `MediaQuery` widget to obtain the screen size of the device using `MediaQueryData`. We then calculate the device width and height and use them to set the width and height of the container that holds the calendar widget.

## Testing the app
Save the changes and run the app using the following command:

```
flutter run
```

You should see a simple app with a responsive calendar widget displayed in the middle of the screen. The width and height of the widget will adjust automatically based on the screen size of the device.

## Conclusion
In this tutorial, we learned how to create a responsive calendar widget using `MediaQuery` in Flutter. By utilizing the device's screen size, we can make our app adapt to different devices and provide a consistent user experience.

Stay tuned for more Flutter tutorials and don't forget to follow #FlutterDev and #MobileAppDevelopment for the latest updates on Flutter and mobile app development. Happy coding!