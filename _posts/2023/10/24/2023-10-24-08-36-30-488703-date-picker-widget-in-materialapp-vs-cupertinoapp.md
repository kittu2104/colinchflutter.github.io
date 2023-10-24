---
layout: post
title: "Date picker widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When it comes to developing cross-platform mobile applications using Flutter, you have two main options for your app's UI: MaterialApp and CupertinoApp. These provide different design styles based on the underlying platform - Material Design for Android-like apps and Cupertino for iOS-like apps.

In this blog post, we will focus on the differences in the date picker widget between MaterialApp and CupertinoApp.

## MaterialApp Date Picker Widget
The date picker widget in MaterialApp is the default Android-styled picker. It follows the Material Design guidelines and provides a consistent user experience across Android devices. To use the date picker widget in MaterialApp, you can utilize the `showDatePicker` method provided by the `showDatePicker` function.

Here's an example of how to use the `showDatePicker` method in MaterialApp:

```dart
import 'package:flutter/material.dart';

class DatePickerPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Date Picker'),
      ),
      body: Center(
        child: RaisedButton(
          onPressed: () {
            showDatePicker(
              context: context,
              initialDate: DateTime.now(),
              firstDate: DateTime(2000),
              lastDate: DateTime(2025),
            );
          },
          child: Text('Show Date Picker'),
        ),
      ),
    );
  }
}
```

## CupertinoApp Date Picker Widget
On the other hand, the date picker widget in CupertinoApp follows the iOS-like design, providing a native iOS experience to your users. To display the date picker in CupertinoApp, you can use the `CupertinoDatePicker` widget.

Here's an example of using `CupertinoDatePicker` in CupertinoApp:

```dart
import 'package:flutter/cupertino.dart';

class DatePickerPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Date Picker'),
      ),
      child: Center(
        child: CupertinoButton(
          onPressed: () {
            showCupertinoModalPopup(
              context: context,
              builder: (BuildContext context) {
                return Container(
                  height: 300,
                  child: CupertinoDatePicker(
                    initialDateTime: DateTime.now(),
                    minimumYear: 2000,
                    maximumYear: 2025,
                    mode: CupertinoDatePickerMode.date,
                    onDateTimeChanged: (DateTime newDateTime) {
                      print(newDateTime);
                    },
                  ),
                );
              },
            );
          },
          child: Text('Show Date Picker'),
        ),
      ),
    );
  }
}
```

As you can see, while the usage of the date picker widget is similar, the appearance and style differ based on the chosen app design. MaterialApp follows Material Design, while CupertinoApp provides an iOS-like experience.

It is essential to choose the appropriate UI style based on the target platform to ensure a consistent and native user experience. Consider the design guidelines of each platform and select the right one for your app.

# Conclusion
In this blog post, we explored the date picker widget in MaterialApp and CupertinoApp. We discussed how to implement it in each design style and highlighted the differences between the two. Remember to choose the UI style that suits your app's target platform to provide a familiar and native experience to your users.