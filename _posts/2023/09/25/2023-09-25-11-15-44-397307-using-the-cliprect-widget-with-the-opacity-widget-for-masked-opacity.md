---
layout: post
title: "Using the ClipRect widget with the Opacity widget for masked opacity"
description: " "
date: 2023-09-25
tags: [flutter]
comments: true
share: true
---

In Flutter, you can use the `ClipRect` widget along with the `Opacity` widget to achieve a masked opacity effect. This effect allows you to control the transparency of a specific area of your widget, while keeping the rest of the widget fully opaque.

## The `ClipRect` Widget

The `ClipRect` widget is used to clip its child widget to the specified rectangular boundary. Any portion of the child widget that falls outside this boundary is clipped away.

Here's an example of how to use `ClipRect`:

```dart
ClipRect(
  child: Container(
    width: 200,  // Width of the clipped area
    height: 200, // Height of the clipped area
    color: Colors.blue,
    child: Text(
      'Hello, Flutter!',
      style: TextStyle(
        fontSize: 24,
        color: Colors.white,
      ),
    ),
  ),
),
```

In this example, the `ClipRect` widget clips the `Container` widget to a rectangular area of 200x200 pixels. The text 'Hello, Flutter!' is displayed within this clipped area.

## The `Opacity` Widget

The `Opacity` widget is used to apply an opacity level to its child widget. The value passed to the `opacity` property determines the transparency level, with `0.0` being completely transparent and `1.0` being fully opaque.

Here's an example of how to use `Opacity`:

```dart
Opacity(
  opacity: 0.5, // Opacity level of 50%
  child: Container(
    width: 200,
    height: 200,
    color: Colors.red,
    child: Text(
      'Masked Opacity',
      style: TextStyle(
        fontSize: 24,
        color: Colors.white,
      ),
    ),
  ),
),
```

In this example, the `Opacity` widget applies a transparency level of 50% to the `Container` widget and its child, making it semi-transparent.

## Combining `ClipRect` and `Opacity` for Masked Opacity

To achieve the masked opacity effect, you can nest the `Opacity` widget inside the `ClipRect` widget. This allows you to control the opacity of a specific area defined by the `ClipRect`.

Here's an example of how to combine `ClipRect` and `Opacity`:

```dart
ClipRect(
  child: Opacity(
    opacity: 0.5, // Opacity level of 50%
    child: Container(
      width: 200,
      height: 200,
      color: Colors.green,
      child: Text(
        'Masked Opacity',
         style: TextStyle(
          fontSize: 24,
          color: Colors.white,
        ),
      ),
    ),
  ),
),
```

In this example, the `ClipRect` widget defines the rectangular boundary for the opacity effect, and the `Opacity` widget applies a transparency level of 50% to the `Container` widget and its child. Only the portion of the widget falling within the `ClipRect` boundary will be affected by the opacity.

By combining the `ClipRect` and `Opacity` widgets in this way, you can achieve a masked opacity effect in your Flutter application.

#flutter #ui