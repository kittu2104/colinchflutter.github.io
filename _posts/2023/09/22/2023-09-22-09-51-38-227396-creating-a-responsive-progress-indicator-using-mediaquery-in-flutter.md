---
layout: post
title: "Creating a responsive progress indicator using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [Flutter, ResponsiveUI]
comments: true
share: true
---

Flutter, a popular UI toolkit, allows developers to create beautiful and interactive applications for various platforms using a single codebase. `MediaQuery` is a powerful tool provided by Flutter that allows you to fetch information about the application's window size and device characteristics.

To create a responsive progress indicator in Flutter, follow these steps:

1. Import the necessary packages:
```
import 'package:flutter/material.dart';
```

2. Create a stateful widget:
```dart
class MyProgressIndicator extends StatefulWidget {
  @override
  _MyProgressIndicatorState createState() => _MyProgressIndicatorState();
}

class _MyProgressIndicatorState extends State<MyProgressIndicator> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Progress Indicator'),
      ),
      body: Center(
        child: Container(
          padding: EdgeInsets.all(16.0),
          child: CircularProgressIndicator(),
        ),
      ),
    );
  }
}
```

3. Wrap the `CircularProgressIndicator` widget with a `Container` and set padding as desired. This container will help us control the size of the progress indicator.

4. Update the `build` method to use `MediaQuery` to determine the screen size and adjust the size of the `CircularProgressIndicator` widget accordingly:
```dart
Widget build(BuildContext context) {
  Size screenSize = MediaQuery.of(context).size;

  return Scaffold(
    appBar: AppBar(
      title: Text('Responsive Progress Indicator'),
    ),
    body: Center(
      child: Container(
        padding: EdgeInsets.all(16.0),
        width: screenSize.width * 0.5,       // Adjust the width based on the screen size
        height: screenSize.height * 0.1,     // Adjust the height based on the screen size
        child: CircularProgressIndicator(),
      ),
    ),
  );
}
```

By using `MediaQuery` to calculate the screen size, we can make the progress indicator responsive based on the device's dimensions. Adjust the width and height as needed to achieve the desired visual appearance.

Remember to add the `MyProgressIndicator` widget to your app's widget tree for it to be displayed:
```dart
void main() {
  runApp(MaterialApp(
    home: MyProgressIndicator(),
  ));
}
```

That's it! You have successfully created a responsive progress indicator using `MediaQuery` in Flutter. Now, your users will have a better experience on various devices as the progress indicator adapts to different screen sizes. 

#Flutter #ResponsiveUI