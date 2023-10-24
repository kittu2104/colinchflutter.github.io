---
layout: post
title: "Radio button widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [radiobutton]
comments: true
share: true
---

When it comes to creating user interfaces in mobile applications, there are multiple choices available. Two popular frameworks for mobile app development are MaterialApp and CupertinoApp, which belong to the Flutter SDK. Each framework offers its own set of widgets and design styles.

In this blog post, we will focus on the radio button widget and explore how it differs in MaterialApp and CupertinoApp.

## Radio Button Widget

A radio button is a UI element that allows users to select a single option from a predefined list of choices. The selected option is visually indicated by a filled circle within the button. Flutter provides a `Radio` widget that can be used to create radio buttons.

### MaterialApp

MaterialApp is a widget that implements the Material Design guidelines for Android-like user interfaces. When using MaterialApp, the radio button widget (`Radio`) follows the Material Design specifications.

Here's an example code snippet on how to use the `Radio` widget in MaterialApp:

```dart
import 'package:flutter/material.dart';

class RadioExample extends StatefulWidget {
  @override
  _RadioExampleState createState() => _RadioExampleState();
}

class _RadioExampleState extends State<RadioExample> {
  int selectedValue;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Radio Button Example')),
        body: Column(
          children: <Widget>[
            Radio(
              value: 1,
              groupValue: selectedValue,
              onChanged: (value) {
                setState(() {
                  selectedValue = value;
                });
              },
            ),
            Radio(
              value: 2,
              groupValue: selectedValue,
              onChanged: (value) {
                setState(() {
                  selectedValue = value;
                });
              },
            ),
          ],
        ),
      ),
    );
  }
}

void main() => runApp(RadioExample());
```

In MaterialApp, the radio buttons have a circular design with a Material Design touch, giving a familiar look and feel to Android users.

### CupertinoApp

CupertinoApp, on the other hand, implements Apple's iOS-style user interfaces based on the Cupertino design system. When using CupertinoApp, the radio button widget (`Radio`) follows the Cupertino Design specifications.

Here's an example code snippet on how to use the `Radio` widget in CupertinoApp:

```dart
import 'package:flutter/cupertino.dart';

class RadioExample extends StatefulWidget {
  @override
  _RadioExampleState createState() => _RadioExampleState();
}

class _RadioExampleState extends State<RadioExample> {
  int selectedValue;

  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('Radio Button Example'),
        ),
        child: Column(
          children: <Widget>[
            Radio(
              value: 1,
              groupValue: selectedValue,
              onChanged: (value) {
                setState(() {
                  selectedValue = value;
                });
              },
            ),
            Radio(
              value: 2,
              groupValue: selectedValue,
              onChanged: (value) {
                setState(() {
                  selectedValue = value;
                });
              },
            ),
          ],
        ),
      ),
    );
  }
}

void main() => runApp(RadioExample());
```

In CupertinoApp, the radio buttons have a circular design with a typical iOS look and feel. This ensures consistency with the native iOS experience.

## Conclusion

Both MaterialApp and CupertinoApp offer widgets that abide by the design guidelines of their respective platforms. When it comes to radio buttons, MaterialApp follows the Material Design guidelines for Android-like interfaces, while CupertinoApp adheres to the Cupertino design system for iOS-like interfaces.

Remember to choose the appropriate framework and widget style based on the target platform to provide an intuitive and consistent user experience.

#flutter #radiobutton