---
layout: post
title: "Snackbar widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [Snackbar]
comments: true
share: true
---

When it comes to building cross-platform mobile applications, Flutter provides two main frameworks: MaterialApp and CupertinoApp. These frameworks offer different sets of widgets that cater to the design guidelines of their respective platforms, namely Material Design for Android (MatieralApp) and Cupertino for iOS (CupertinoApp).

One popular widget that exists in both MaterialApp and CupertinoApp is the Snackbar widget. A Snackbar is a temporary notification that appears at the bottom of the screen and provides feedback or alerts to the user.

### Snackbar in MaterialApp

To use the Snackbar widget in MaterialApp, you need to have a Scaffold widget, as it provides the necessary context for the Snackbar to be displayed. Here's an example:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('MaterialApp Snackbar Example'),
      ),
      body: Center(
        child: ElevatedButton(
          child: Text('Show Snackbar'),
          onPressed: () {
            ScaffoldMessenger.of(context).showSnackBar(
              SnackBar(
                content: Text('Hello from MaterialApp Snackbar!'),
              ),
            );
          },
        ),
      ),
    ),
  ));
}
```

In the example above, we wrap our application with MaterialApp and place a Scaffold as the home widget. Inside the Scaffold's body, we have a button that triggers the display of the Snackbar when pressed. We use `ScaffoldMessenger.of(context).showSnackBar()` to show the Snackbar.

### Snackbar in CupertinoApp

Similarly, to use the Snackbar widget in CupertinoApp, you need to have a CupertinoPageScaffold widget, which provides the necessary context. Here's an example:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('CupertinoApp Snackbar Example'),
      ),
      child: Center(
        child: CupertinoButton(
          child: Text('Show Snackbar'),
          onPressed: () {
            ScaffoldMessenger.of(context).showSnackBar(
              SnackBar(
                content: Text('Hello from CupertinoApp Snackbar!'),
              ),
            );
          },
        ),
      ),
    ),
  ));
}
```

In this example, we wrap our application with CupertinoApp and place a CupertinoPageScaffold as the home widget. Inside the CupertinoPageScaffold's child, we have a button that triggers the display of the Snackbar when pressed. Again, we use `ScaffoldMessenger.of(context).showSnackBar()` to show the Snackbar.

### Conclusion

The Snackbar widget is a useful and commonly used component for displaying temporary notifications in Flutter applications. Whether you are developing for Android or iOS, Flutter's MaterialApp and CupertinoApp frameworks provide seamless integration of the Snackbar widget. By understanding the differences in their usage within each framework, you can create consistent and platform-specific user experiences. So, depending on the platform you are targeting, choose the appropriate framework and create amazing snackbar notifications!

*Tags: #Flutter #Snackbar*