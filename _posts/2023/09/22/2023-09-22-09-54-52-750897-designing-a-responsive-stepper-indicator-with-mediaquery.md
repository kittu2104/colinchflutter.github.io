---
layout: post
title: "Designing a responsive stepper indicator with `MediaQuery`"
description: " "
date: 2023-09-22
tags: []
comments: true
share: true
---

In this blog post, we will explore how to design a responsive stepper indicator using `MediaQuery` in order to provide a smooth user experience across different screen sizes.

## What is a Stepper Indicator?

A stepper indicator is a visual representation of a step-by-step process. It is often used in applications where users need to complete a series of tasks or stages. The stepper indicator helps users track their progress and provides feedback on which step they are currently on.

## Designing the Stepper Indicator

To design a responsive stepper indicator, we need to consider the different screen sizes and adjust the layout accordingly. We can achieve this by utilizing the `MediaQuery` widget in Flutter, which allows us to customize the layout based on the device's screen size.

### Step 1: Import the required packages

To get started, we need to import the necessary packages in our Flutter application. In your `pubspec.yaml` file, add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter

  flutter_screenutil: ^4.0.2
```

Then, run `flutter pub get` to install the packages.

### Step 2: Create a responsive layout

To create a responsive layout, we will use the `MediaQuery` widget to retrieve the screen size and adjust the layout accordingly.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';

class StepperIndicator extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    ScreenUtil.init(context);

    return Scaffold(
      appBar: AppBar(
        title: Text('Stepper Indicator'),
      ),
      body: SingleChildScrollView(
        child: Column(
          children: [
            Container(
              width: 0.9.sw, // Adjust the width based on the screen size
              height: 80.h, // Adjust the height based on the screen size
              color: Colors.grey,
              child: Row(
                mainAxisAlignment: MainAxisAlignment.spaceEvenly,
                children: [
                  Container(
                    width: 30.w,
                    height: 30.h,
                    decoration: BoxDecoration(
                      shape: BoxShape.circle,
                      color: Colors.green,
                    ),
                  ),
                  Container(
                    width: 30.w,
                    height: 30.h,
                    decoration: BoxDecoration(
                      shape: BoxShape.circle,
                      color: Colors.grey,
                    ),
                  ),
                  Container(
                    width: 30.w,
                    height: 30.h,
                    decoration: BoxDecoration(
                      shape: BoxShape.circle,
                      color: Colors.grey,
                    ),
                  ),
                ],
              ),
            ),
            SizedBox(height: 20.h),
            Text(
              'Step 1 of 3',
              style: TextStyle(
                fontSize: 20.sp,
                fontWeight: FontWeight.bold,
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

### Step 3: Testing the Stepper Indicator

To test the stepper indicator, we can simply navigate to the desired screen in our Flutter application and add the `StepperIndicator` widget. The layout will automatically adjust based on the screen size.

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Stepper Indicator',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: StepperIndicator(),
    );
  }
}
```

## Conclusion

Designing a responsive stepper indicator is essential for creating a user-friendly interface across different devices. By utilizing the `MediaQuery` widget in Flutter, we can easily customize the layout based on the screen size. This ensures a consistent user experience and makes it easier for users to track their progress.