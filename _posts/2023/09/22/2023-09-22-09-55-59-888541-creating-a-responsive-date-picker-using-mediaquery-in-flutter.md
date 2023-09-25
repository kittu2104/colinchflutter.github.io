---
layout: post
title: "Creating a responsive date picker using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [datePicker]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive date picker in Flutter using the `MediaQuery` class. The date picker will adjust its appearance based on the screen size of the device it is being displayed on.

### Step 1: Import the necessary packages

To create a date picker in Flutter, we need to import the following package:

```dart
import 'package:flutter/material.dart';
```

### Step 2: Create a Stateless Widget

Next, let's create a stateless widget called `ResponsiveDatePicker` that extends `StatelessWidget`. This widget will be responsible for rendering the date picker:

```dart
class ResponsiveDatePicker extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      // Your date picker UI code goes here
    );
  }
}
```

### Step 3: Implement the Date Picker UI

Inside the `build` method of the `ResponsiveDatePicker` widget, we can define our date picker UI. We will use a `MediaQuery` to determine the screen size and adjust the layout accordingly:

```dart
@override
Widget build(BuildContext context) {
  bool isLargeScreen = MediaQuery.of(context).size.width > 600;

  return Container(
    padding: const EdgeInsets.all(16.0),
    child: isLargeScreen
        ? _buildDesktopDatePicker()
        : _buildMobileDatePicker(),
  );
}

Widget _buildDesktopDatePicker() {
  // UI code for desktop layout
}

Widget _buildMobileDatePicker() {
  // UI code for mobile layout
}
```

### Step 4: Implement the Date Selection Logic

Now, let's implement the logic for selecting a date. We can use the `showDatePicker` method provided by the Flutter framework:

```dart
void _selectDate(BuildContext context) async {
  final DateTime? picked = await showDatePicker(
    context: context,
    initialDate: DateTime.now(),
    firstDate: DateTime(2000),
    lastDate: DateTime(2100),
  );

  if (picked != null) {
    // Do something with the selected date
  }
}
```

### Step 5: Use the Date Picker in your App

Finally, we can use our `ResponsiveDatePicker` widget in our app's UI. For example, we can add a button that triggers the date picker upon pressing:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My App',
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Date Picker'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () => _selectDate(context),
            child: Text('Select Date'),
          ),
        ),
      ),
    );
  }
}

void main() {
  runApp(MyApp());
}
```

### Conclusion

In this tutorial, we have learned how to create a responsive date picker using the `MediaQuery` class in Flutter. By leveraging the screen size of the device, we can provide an optimal user experience across different devices and orientations.

#flutter #datePicker