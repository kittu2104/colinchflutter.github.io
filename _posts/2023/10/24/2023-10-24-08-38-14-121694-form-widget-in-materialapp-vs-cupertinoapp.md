---
layout: post
title: "Form widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [materialdesign, cupertino]
comments: true
share: true
---

When creating a form in Flutter, you have the option to use either the `MaterialApp` or `CupertinoApp` widget, depending on the design language you want to follow - Material Design or Cupertino (iOS) design.

## Using MaterialApp

If you are developing an app with the Material Design guidelines, you would typically use the `MaterialApp` widget to create your app's main entry point. The `MaterialApp` provides the overall Material Design app structure and includes various material-themed widgets.

To create a form using `MaterialApp`, you can use the `Form` widget along with other form-related widgets such as `TextFormField` and `RaisedButton`. Here's an example:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('My Form'),
      ),
      body: Center(
        child: Form(
          child: Column(
            children: [
              TextFormField(
                decoration: InputDecoration(labelText: 'Username'),
              ),
              TextFormField(
                decoration: InputDecoration(labelText: 'Password'),
              ),
              RaisedButton(
                child: Text('Submit'),
                onPressed: () {},
              ),
            ],
          ),
        ),
      ),
    ),
  ));
}
```

In this example, the `MaterialApp` is used as the root widget, and the `Form` widget is added as the main content of the `Scaffold` widget. The individual form fields, like `TextFormField`, are added within the `Form` to collect user input.

## Using CupertinoApp

If you are targeting your app specifically for iOS devices and want to follow the native iOS design, you can use the `CupertinoApp` widget. The `CupertinoApp` provides the overall Cupertino-style app structure, along with Cupertino-themed widgets.

To create a form using `CupertinoApp`, you can use the `CupertinoFormSection`, `CupertinoTextField`, and `CupertinoButton` widgets. Here's an example:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('My Form'),
      ),
      child: Center(
        child: CupertinoFormSection(
          children: [
            CupertinoTextFormFieldRow(
              placeholder: 'Username',
            ),
            CupertinoTextFormFieldRow(
              placeholder: 'Password',
            ),
            CupertinoButton(
              child: Text('Submit'),
              onPressed: () {},
            ),
          ],
        ),
      ),
    ),
  ));
}
```

In this example, the `CupertinoApp` is used as the root widget, and the `CupertinoPageScaffold` is added as the main content. The form-related widgets, such as `CupertinoFormSection` and `CupertinoTextFormFieldRow`, are used to create the form fields.

## Conclusion

Deciding between using the `MaterialApp` or `CupertinoApp` for forms in Flutter depends on the design language you want to follow. If you want your app to adhere to Material Design guidelines, use `MaterialApp`, and if you prefer a native iOS design, use `CupertinoApp`. Both widgets provide form-related components that you can use to create user-friendly and visually cohesive forms in your Flutter app.

#flutter #materialdesign #cupertino