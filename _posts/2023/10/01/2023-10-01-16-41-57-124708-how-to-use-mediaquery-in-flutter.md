---
layout: post
title: "How to use MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [ResponsiveUI]
comments: true
share: true
---

In Flutter, `MediaQuery` class allows you to retrieve information about the current device's screen size, orientation, and other metrics. By utilizing `MediaQuery`, you can create responsive UIs that adapt to different screen sizes and orientations.

## Retrieving Screen Size

To retrieve the size of the screen, you can use the `MediaQuery.of(context).size` property. This property returns a `Size` object containing the width and height of the screen.

```dart
Size screenSize = MediaQuery.of(context).size;
double screenWidth = screenSize.width;
double screenHeight = screenSize.height;
```

You can then use these values to create responsive layouts that adjust based on the available screen space.

## Responsive Layouts

Flutter provides various widgets that allow you to create responsive layouts using `MediaQuery`. For example, the `FractionallySizedBox` widget is useful for creating layouts that adapt to the available screen space:

```dart
FractionallySizedBox(
  widthFactor: 0.8, // Adjust the width based on the screen size
  child: Container(
    color: Colors.blue,
    child: Text(
      'Responsive Text',
      style: TextStyle(fontSize: 20),
    ),
  ),
),
```

In the above example, the `widthFactor` property of `FractionallySizedBox` is set to `0.8`, which means the container will occupy 80% of the available screen width. This ensures the layout adapts based on different screen sizes.

## Responsive Styling

You can also use `MediaQuery` to apply responsive styling to your widgets. For example, you can set the font size based on the screen width:

```dart
double screenWidth = MediaQuery.of(context).size.width;
double fontSize = screenWidth > 600 ? 20 : 16;

Text(
  'Responsive Text',
  style: TextStyle(fontSize: fontSize),
),
```

In the above code snippet, the font size is set to `20` if the screen width is greater than `600`, otherwise it is set to `16`. By using `MediaQuery`, you can ensure consistent styling across different devices.

## Conclusion

Using `MediaQuery` in Flutter allows you to create responsive UIs that adapt to different screen sizes and orientations. By retrieving the screen size and other metrics, you can create layouts and apply styling that adjusts based on the available screen space. This ensures a better user experience across various devices and screen sizes.

#Flutter #ResponsiveUI