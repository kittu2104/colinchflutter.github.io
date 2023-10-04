---
layout: post
title: "MediaQuery width in Flutter"
description: " "
date: 2023-10-01
tags: [mediaquery]
comments: true
share: true
---

When working with responsive layouts in Flutter, you may need to determine the width of the device's screen or the available width within a certain widget. This can be achieved using the `MediaQuery` class provided by Flutter.

The `MediaQuery` class allows you to access various information about the device's screen, such as its size, orientation, and pixel density. To get the width of the device's screen, you can use the `MediaQuery.of(context).size.width` property.

Here's an example code snippet that demonstrates how to retrieve the device's screen width:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    double screenWidth = MediaQuery.of(context).size.width;

    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Layout'),
      ),
      body: Center(
        child: Text(
          'Device Width: $screenWidth',
          style: TextStyle(
            fontSize: 20.0,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
```

In this example, we import the `flutter/material.dart` package and define a stateless widget called `MyWidget`. Inside the `build` method, we retrieve the device's screen width using the `MediaQuery.of(context).size.width` property and store it in the `screenWidth` variable.

Finally, we create a `Center` widget and display the device width using a `Text` widget. The screen width is passed as a string interpolation to the `Text` widget's `data` parameter.

Remember to wrap your widgets with a `MaterialApp` or `WidgetsApp` in order to access the `MediaQuery` information.

Keep in mind that the width obtained from `MediaQuery` may not account for any padding or constraints applied to the widget. If you need to get the available width within a specific widget, you can use `MediaQuery.of(context).size.width` within that widget's context.

By using `MediaQuery` and accessing the device's screen width, you can make your Flutter app more responsive and adaptive to different screen sizes.

#flutter #mediaquery