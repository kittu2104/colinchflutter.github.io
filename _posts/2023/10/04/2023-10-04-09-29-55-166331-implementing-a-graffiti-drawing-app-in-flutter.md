---
layout: post
title: "Implementing a graffiti drawing app in Flutter"
description: " "
date: 2023-10-04
tags: [setting, creating]
comments: true
share: true
---

In this tutorial, we will learn how to create a graffiti drawing app using Flutter, a popular cross-platform framework for building mobile applications. The app will allow users to draw on the screen using their finger and customize the drawing with various colors and brush sizes.

## Table of Contents
- [Setting Up the Project](#setting-up-the-project)
- [Creating the Drawing Canvas](#creating-the-drawing-canvas)
- [Handling User Input](#handling-user-input)
- [Customizing Colors and Brush Sizes](#customizing-colors-and-brush-sizes)
- [Saving and Sharing Drawings](#saving-and-sharing-drawings)

## Setting Up the Project

First, we need to set up a new Flutter project. Open your preferred IDE or text editor and create a new Flutter project using the command-line tools or IDE plugins.

## Creating the Drawing Canvas

To create the drawing canvas, we will use a `CustomPaint` widget. This widget allows us to paint custom content on the screen. Add the following code to the `build()` method of your main `Widget`:

```dart
CustomPaint(
  painter: DrawingPainter(),
  child: GestureDetector(
    onPanUpdate: (details) {
      // TODO: Handle drawing logic
    },
  ),
)
```

The `CustomPaint` widget takes a `painter` argument, which is responsible for painting the content on the screen. We will create a custom `DrawingPainter` class for this purpose.

## Handling User Input

Inside the `onPanUpdate` callback of the `GestureDetector`, we will handle the user's finger movements to draw on the canvas. Add the following code to the `onPanUpdate` callback:

```dart
onPanUpdate: (details) {
  setState(() {
    // TODO: Update drawing logic based on details.delta
  });
}
```

The `details.delta` contains the distance the user's finger has moved since the last update. We will use this information to update the drawing logic.

## Customizing Colors and Brush Sizes

To allow users to customize the drawing color and brush size, we can use a combination of `ColorPicker` and `Slider` widgets. Add these widgets to your app's UI, and use their values to update the drawing color and brush size in the `DrawingPainter` class.

## Saving and Sharing Drawings

To save and share the drawings, we can use the `image_gallery_saver` and `share` packages. These packages allow us to save the drawn image to the device's gallery and share it with other apps. Install these packages and implement the logic to save and share the drawing.

```dart
// Saving the drawing
final bytes = await rootBundle.load('assets/drawing.png');
final result = await ImageGallerySaver.saveImage(
  Uint8List.view(bytes.buffer),
  name: 'drawing',
);

// Sharing the drawing
final filePath = result['filePath'];
await Share.shareFiles([filePath], text: 'Check out my drawing!');
```

## Conclusion

In this tutorial, we have learned how to implement a graffiti drawing app using Flutter. We have explored creating the drawing canvas, handling user input, customizing colors and brush sizes, and saving and sharing drawings. With these concepts, you can now create your own drawing app or enhance the functionality of existing apps. Happy coding!

#### #flutter #drawingapp