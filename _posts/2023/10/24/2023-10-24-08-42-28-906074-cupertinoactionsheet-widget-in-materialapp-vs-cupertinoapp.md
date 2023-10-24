---
layout: post
title: "CupertinoActionSheet widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---
In Flutter, CupertinoActionSheet is a widget that displays a modal action sheet on the screen, similar to the behavior of the iOS action sheet. 

## Using CupertinoActionSheet in MaterialApp
To use the CupertinoActionSheet widget in a MaterialApp, you need to wrap your entire app in a MaterialApp widget. MaterialApp is a convenience widget that wraps several other widgets, such as MaterialApp's title, theme, and routes. 

Here's an example of using CupertinoActionSheet in a MaterialApp:

```dart
import 'package:flutter/material.dart';
import 'package:flutter/cupertino.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'CupertinoActionSheet Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('CupertinoActionSheet Demo'),
        ),
        body: Center(
          child: RaisedButton(
            child: Text('Show Action Sheet'),
            onPressed: () {
              showCupertinoModalPopup(
                context: context,
                builder: (BuildContext context) {
                  return CupertinoActionSheet(
                    title: Text('Select an option'),
                    actions: <Widget>[
                      CupertinoActionSheetAction(
                        onPressed: () {
                          // Perform action
                        },
                        child: Text('Option 1'),
                      ),
                      CupertinoActionSheetAction(
                        onPressed: () {
                          // Perform action
                        },
                        child: Text('Option 2'),
                      ),
                      CupertinoActionSheetAction(
                        onPressed: () {
                          // Perform action
                        },
                        child: Text('Option 3'),
                      ),
                    ],
                    cancelButton: CupertinoActionSheetAction(
                      onPressed: () {
                        Navigator.pop(context);
                      },
                      child: Text('Cancel'),
                    ),
                  );
                },
              );
            },
          ),
        ),
      ),
    );
  }
}
```

In this example, we use the `showCupertinoModalPopup` method to display the `CupertinoActionSheet` when the `Show Action Sheet` button is pressed. The `CupertinoActionSheet` widget contains a title, a list of actions, and a cancel button.

## Using CupertinoActionSheet in CupertinoApp
Alternatively, you can also use the `CupertinoActionSheet` widget in a `CupertinoApp`. The `CupertinoApp` widget is similar to `MaterialApp`, but it sets the iOS-specific Cupertino theme for your app.

Here's an example of using `CupertinoActionSheet` in a `CupertinoApp`:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      title: 'CupertinoActionSheet Demo',
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('CupertinoActionSheet Demo'),
        ),
        child: Center(
          child: CupertinoButton(
            child: Text('Show Action Sheet'),
            onPressed: () {
              showCupertinoModalPopup(
                context: context,
                builder: (BuildContext context) {
                  return CupertinoActionSheet(
                    title: Text('Select an option'),
                    actions: <Widget>[
                      CupertinoActionSheetAction(
                        onPressed: () {
                          // Perform action
                        },
                        child: Text('Option 1'),
                      ),
                      CupertinoActionSheetAction(
                        onPressed: () {
                          // Perform action
                        },
                        child: Text('Option 2'),
                      ),
                      CupertinoActionSheetAction(
                        onPressed: () {
                          // Perform action
                        },
                        child: Text('Option 3'),
                      ),
                    ],
                    cancelButton: CupertinoActionSheetAction(
                      onPressed: () {
                        Navigator.pop(context);
                      },
                      child: Text('Cancel'),
                    ),
                  );
                },
              );
            },
          ),
        ),
      ),
    );
  }
}
```

In this example, we wrap our app in the `CupertinoApp` widget and use `CupertinoPageScaffold` to set up the basic structure of our app. The `CupertinoNavigationBar` at the top serves as our app bar, and the `CupertinoButton` is used to trigger the display of the `CupertinoActionSheet`.

# Conclusion
Both `MaterialApp` and `CupertinoApp` can be used to display `CupertinoActionSheet` in Flutter. If you're targeting iOS devices specifically and want to use the iOS-specific Cupertino theme, the `CupertinoApp` would be a better choice. Otherwise, if you're developing a cross-platform app, you can use `MaterialApp` and still achieve a similar behavior with `CupertinoActionSheet`.