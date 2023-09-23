---
layout: post
title: "Implementing responsive image zooming using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, responsiveimagetzoom]
comments: true
share: true
---

Images are an important part of any app and providing an interactive and engaging way to view images can greatly enhance the user experience. One such feature is image zooming, where users can zoom in and out of an image to view it in more detail.

In Flutter, we can implement responsive image zooming using the `MediaQuery` class, which allows us to retrieve information about the current device's screen size and orientation.

## Setting up the project

Before we start implementing the image zooming functionality, let's create a basic Flutter project. Open your terminal and run the following command:

```dart
flutter create responsive_image_zoom
cd responsive_image_zoom
```

Now, open the `lib/main.dart` file in your preferred code editor.

## Adding an image widget

First, let's add an image widget to our app. Replace the default code in `main.dart` with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Image Zoom',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Image Zoom'),
        ),
        body: Center(
          child: Image.network(
            'https://example.com/image.jpg',
            width: 300,
          ),
        ),
      ),
    );
  }
}
```

In the above code, we have added an `Image` widget to the center of the `Scaffold` widget. Make sure to replace the `https://example.com/image.jpg` URL with the actual URL of the image you want to display.

## Implementing image zooming

Now, let's implement the image zooming functionality using `MediaQuery`. We'll wrap the `Image` widget inside a `GestureDetector` widget to detect user gestures.

Replace the `Image` widget code with the following code:

```dart
GestureDetector(
  onScaleUpdate: (ScaleUpdateDetails details) {
    double newScale = details.scale.clamp(1.0, 5.0);

    // Update the UI
    setState(() {
      _scale = newScale;
    });
  },
  child: Transform.scale(
    scale: _scale,
    child: Image.network(
      'https://example.com/image.jpg',
      width: 300,
    ),
  ),
)
```

In the code above, we have added an `onScaleUpdate` callback to the `GestureDetector` widget. This callback is triggered when the user performs a scaling gesture (e.g., pinch-to-zoom). We clamp the scale value between 1.0 and 5.0 to limit the zooming range.

Inside the callback, we update the `_scale` variable and call `setState` to notify Flutter to update the UI.

Finally, we wrap the `Image` widget inside a `Transform.scale` widget and set the scale value to `_scale`. This applies the zooming effect to the image based on the current scale value.

## Making the image responsive

Flutter provides `MediaQuery` to make the UI responsive to different screen sizes and orientations. We can use it to dynamically adjust the image size based on the available screen width.

Wrap the `Transform.scale` widget with the following code:

```dart
LayoutBuilder(
  builder: (BuildContext context, BoxConstraints constraints) {
    double width = constraints.maxWidth;

    return Transform.scale(
      scale: _scale,
      child: Image.network(
        'https://example.com/image.jpg',
        width: width,
      ),
    );
  },
)
```

In the code above, we wrap the `Transform.scale` widget inside a `LayoutBuilder` widget. The `LayoutBuilder` widget provides us with the current constraints of the parent widget.

Inside the `builder` callback, we extract the maximum width from the constraints and assign it to the `width` variable. We then pass this width value to the `Image` widget using the `width` property, making the image responsive to different screen sizes.

## Conclusion

By combining `MediaQuery` with `GestureDetector` and `Transform.scale`, we can implement responsive image zooming in Flutter. Users can now zoom in and out of the image by performing scaling gestures, and the image size adjusts responsively based on the screen width.

Make sure to optimize your image sizes and consider lazy loading for better performance and user experience.

#flutter #responsiveimagetzoom