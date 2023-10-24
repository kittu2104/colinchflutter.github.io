---
layout: post
title: "Cupertino time picker customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When it comes to customizing the Cupertino Time Picker in your Flutter application, you have two options: MaterialApp or CupertinoApp. In this blog post, we will discuss the differences and advantages of using each approach.

## Using MaterialApp

If your app is primarily designed with Material Design in mind, using MaterialApp for customization would be the logical choice. The MaterialApp widget provides a Material-style Cupertino Time Picker, which fits seamlessly with the overall look and feel of your app. 

Here's an example of how you can customize the Cupertino Time Picker within a MaterialApp:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: HomeScreen(),
    theme: ThemeData(
      // Customize your app's primary color
      primaryColor: Colors.blue,
    ),
  ));
}

class HomeScreen extends StatefulWidget {
  @override
  _HomeScreenState createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  TimeOfDay _time = TimeOfDay.now();

  void _selectTime(BuildContext context) async {
    final TimeOfDay? newTime = await showTimePicker(
      context: context,
      initialTime: _time,
    );

    if (newTime != null) {
      setState(() {
        _time = newTime;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Custom Time Picker'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'Selected time: ${_time.format(context)}',
              style: TextStyle(fontSize: 20),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () => _selectTime(context),
              child: Text('Select Time'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Using CupertinoApp

On the other hand, if you want to create a Cupertino-style app or prefer to maintain a consistent iOS look and feel throughout your application, using CupertinoApp for customization would be the way to go. This comes with the advantage of having a native iOS-like Cupertino Time Picker.

To customize the Cupertino Time Picker using the CupertinoApp widget, you can follow this example:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: HomeScreen(),
    theme: CupertinoThemeData(
      // Customize your app's primary color
      primaryColor: CupertinoColors.activeBlue,
    ),
  ));
}

class HomeScreen extends StatefulWidget {
  @override
  _HomeScreenState createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  late TimeOfDay _time;

  @override
  void initState() {
    super.initState();
    _time = TimeOfDay.now();
  }

  void _selectTime(BuildContext context) async {
    final TimeOfDay? newTime = await showCupertinoModalPopup<TimeOfDay>(
      context: context,
      builder: (BuildContext context) {
        return CupertinoDatePicker(
          mode: CupertinoDatePickerMode.time,
          initialDateTime: DateTime.now(),
          onDateTimeChanged: (DateTime newDateTime) {
            setState(() {
              _time = TimeOfDay.fromDateTime(newDateTime);
            });
          },
        );
      },
    );

    if (newTime != null) {
      setState(() {
        _time = newTime;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Custom Time Picker'),
      ),
      child: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              'Selected time: ${_time.format(context)}',
              style: TextStyle(fontSize: 20),
            ),
            SizedBox(height: 20),
            CupertinoButton(
              onPressed: () => _selectTime(context),
              child: Text('Select Time'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Conclusion

In conclusion, when customizing the Cupertino Time Picker in your Flutter application, you have the option to use either MaterialApp or CupertinoApp. If you want to maintain a consistent Material Design look and feel throughout your app, MaterialApp would be suitable. On the other hand, if you prefer a native iOS-like experience, CupertinoApp is the way to go.

So choose the approach that aligns with your app's design and platform preferences and customize the Cupertino Time Picker accordingly. Happy coding!

---

References:
- [Flutter Documentation: MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter Documentation: CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)
- [Flutter Documentation: CupertinoDatePicker](https://api.flutter.dev/flutter/cupertino/CupertinoDatePicker-class.html)