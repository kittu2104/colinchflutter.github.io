---
layout: post
title: "Cupertino slider colors in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [mobile]
comments: true
share: true
---

When developing a mobile app using Flutter, you have the flexibility to choose between two popular app design styles: Material Design and Cupertino Design. With Material Design, you can use the `MaterialApp` widget, while with Cupertino Design, you can use the `CupertinoApp` widget.

One noticeable difference between the two design styles is how the slider widget is styled. In this article, we will explore the differences in slider colors between `MaterialApp` and `CupertinoApp` and discuss how to customize the slider color in each design style.

## Slider Colors in MaterialApp

When using the `MaterialApp` widget, the slider color follows the default Material Design guidelines. The slider's active track color is determined by the primary color of the app, while the inactive track color is set to a shade of the primary color. The thumb (handle) of the slider also reflects the primary color.

To customize the slider color in `MaterialApp`, you can modify the primary color of your app. This can be done by defining a `ThemeData` object and specifying the primary color. Here's an example:

```dart
MaterialApp(
  theme: ThemeData(
    primaryColor: Colors.blue, // Set primary color to blue
  ),
  // Rest of your app code...
)
```

By setting the primary color to `Colors.blue`, the slider's active track color, inactive track color, and thumb color will all be blue.

## Slider Colors in CupertinoApp

On the other hand, when using the `CupertinoApp` widget, the slider color complies with the default Cupertino Design guidelines. The active track color in this design is a shade of blue, while the inactive track color is gray. The thumb color reflects the primary color of the app.

Customizing the slider color in `CupertinoApp` involves modifying the primary color of your app as well. Here's an example:

```dart
CupertinoApp(
  theme: CupertinoThemeData(
    primaryColor: CupertinoColors.blue, // Set primary color to blue
  ),
  // Rest of your app code...
)
```

By setting the primary color to `CupertinoColors.blue`, the slider's active track color, inactive track color, and thumb color will all be shades of blue.

## Conclusion

In summary, the slider colors in `MaterialApp` and `CupertinoApp` follow the default guidelines of their respective design styles. To customize the slider color, you need to modify the primary color of your app by setting it in the `theme` property of `MaterialApp` or `CupertinoApp`.

Remember, the `MaterialApp` utilizes Material Design, while the `CupertinoApp` adheres to the Cupertino Design. Choose the design style that matches your app's overall look and feel, and customize the slider colors accordingly.

#flutter #mobile-ui