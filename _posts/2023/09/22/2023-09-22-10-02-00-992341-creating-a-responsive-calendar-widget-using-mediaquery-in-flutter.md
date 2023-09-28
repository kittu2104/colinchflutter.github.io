---
layout: post
title: "Creating a responsive calendar widget using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [ResponsiveCalendar]
comments: true
share: true
---

In this blog post, we'll explore how to create a responsive calendar widget using `MediaQuery` in Flutter. With `MediaQuery`, we can easily adapt our widget's appearance and behavior based on the device's screen size and orientation.

## Understanding MediaQuery

`MediaQuery` is a class in Flutter that provides access to the device's screen size and orientation. It allows us to make our widgets responsive, ensuring a consistent user experience across different devices.

## Setting up the Project

Before we start building the widget, let's create a new Flutter project and set up the necessary dependencies. Run the following commands in your terminal:

```
flutter create responsive_calendar
cd responsive_calendar
```

Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  table_calendar: ^3.0.1
```

Save the file, and then run the following command to download the dependencies:

```
flutter pub get
```

## Building the Calendar Widget

Now that our project is set up, let's build the responsive calendar widget. In this example, we'll use the `table_calendar` package, which provides a customizable calendar widget for Flutter.

Start by creating a new `calendar_widget.dart` file in the `lib` directory of your Flutter project. Add the following code to create a basic calendar widget:

```dart
import 'package:flutter/material.dart';

class CalendarWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return TableCalendar(
      calendarStyle: CalendarStyle(
        // Customize the calendar's appearance
      ),
      headerStyle: HeaderStyle(
        // Customize the header's appearance
      ),
      calendarFormat: CalendarFormat.month,
      // Add more configurations as needed
    );
  }
}
```

## Making the Widget Responsive

To make our calendar widget responsive, we need to use `MediaQuery` to retrieve the device's screen size and adjust the widget's properties accordingly. Update the `build` method of the `CalendarWidget` class as follows:

```dart
@override
Widget build(BuildContext context) {
  final double screenWidth = MediaQuery.of(context).size.width;
  final double screenHeight = MediaQuery.of(context).size.height;

  final bool isLandscape = screenHeight < screenWidth;

  return TableCalendar(
    calendarStyle: isLandscape
        ? CalendarStyle(
            // Customize the calendar's appearance for landscape mode
          )
        : CalendarStyle(
            // Customize the calendar's appearance for portrait mode
          ),
    headerStyle: isLandscape
        ? HeaderStyle(
            // Customize the header's appearance for landscape mode
          )
        : HeaderStyle(
            // Customize the header's appearance for portrait mode
          ),
    calendarFormat: CalendarFormat.month,
    // Add more configurations as needed
  );
}
```

In the updated code, we retrieve the device's screen size using `MediaQuery.of(context).size.width` and `MediaQuery.of(context).size.height`. We then determine if the device is in landscape mode by comparing the screen height and width.

Based on the orientation, we customize the appearance of the `calendarStyle` and `headerStyle` properties of the `TableCalendar` widget. You can add more configurations as needed to suit your design requirements.

## Conclusion

In this blog post, we've learned how to create a responsive calendar widget using `MediaQuery` in Flutter. By adapting the widget's appearance and behavior based on the device's screen size and orientation, we provide a consistent user experience across different devices.

With this knowledge, you can now build responsive widgets in your Flutter projects efficiently. Happy coding!

#Flutter #ResponsiveCalendar