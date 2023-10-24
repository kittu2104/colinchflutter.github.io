---
layout: post
title: "Dropdown menu in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [DropdownMenu]
comments: true
share: true
---

In Flutter, you have the option to use either the `MaterialApp` or `CupertinoApp` as the root widget for your app. These two widgets provide different platform-specific designs and components. One such component is the dropdown menu, which behaves differently in each app widget.

## Dropdown menu in MaterialApp
The dropdown menu in the `MaterialApp` widget follows the Material Design guidelines. It presents a menu of options when the user taps on a dropdown button. The selected option is displayed on the button, and when tapped, it opens the menu with a list of available options.

To create a dropdown menu in MaterialApp, you can use the `DropdownButton` widget from the [flutter/material](https://api.flutter.dev/flutter/material/material-library.html) library. Here's an example code snippet:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Dropdown Menu'),
        ),
        body: Center(
          child: DropdownButton<String>(
            items: <String>['Option 1', 'Option 2', 'Option 3']
                .map((String value) {
              return DropdownMenuItem<String>(
                value: value,
                child: Text(value),
              );
            }).toList(),
            onChanged: (String newValue) {
              // Perform actions based on the selected value
            },
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

## Dropdown menu in CupertinoApp
The dropdown menu in the `CupertinoApp` widget follows the Cupertino design guidelines, which are used on iOS devices. It displays a modal sheet with a list of options when tapped. The selected option is also displayed below the dropdown button.

To create a dropdown menu in CupertinoApp, you can use the `CupertinoPicker` widget from the [flutter/cupertino](https://api.flutter.dev/flutter/cupertino/cupertino-library.html) library. Here's an example code snippet:

```dart
import 'package:flutter/cupertino.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('Dropdown Menu'),
        ),
        child: Center(
          child: GestureDetector(
            onTap: () {
              showCupertinoModalPopup(
                context: context,
                builder: (BuildContext context) {
                  return CupertinoPicker(
                    children: <Widget>[
                      Text('Option 1'),
                      Text('Option 2'),
                      Text('Option 3'),
                    ],
                    onSelectedItemChanged: (int index) {
                      // Perform actions based on the selected index
                    },
                  );
                },
              );
            },
            child: Text('Tap to open dropdown'),
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

## Conclusion
Depending on the platform you are targeting, you can choose between the `MaterialApp` and `CupertinoApp` widgets to create your app. The dropdown menu in `MaterialApp` follows Material Design guidelines, while the dropdown menu in `CupertinoApp` follows Cupertino's iOS design guidelines. Choose the widget and dropdown menu style that aligns with your target platform to create a seamless user experience.

#### #Flutter #DropdownMenu