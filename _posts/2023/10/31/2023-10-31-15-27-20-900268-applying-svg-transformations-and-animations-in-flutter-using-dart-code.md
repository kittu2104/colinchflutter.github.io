---
layout: post
title: "Applying SVG transformations and animations in Flutter using Dart code"
description: " "
date: 2023-10-31
tags: [scale, animating]
comments: true
share: true
---

In this blog post, we will explore how to apply SVG transformations and animations in Flutter using Dart code. Scalable Vector Graphics (SVG) is an XML-based file format for describing two-dimensional vector graphics. With Flutter, we can leverage its capabilities to create interactive and animated UI elements.

## Table of Contents
1. [What is SVG?](#what-is-svg)
2. [SVG Transformations](#svg-transformations)
    - [Translate Transform](#translate-transform)
    - [Rotate Transform](#rotate-transform)
    - [Scale Transform](#scale-transform)
3. [Animating SVG in Flutter](#animating-svg-in-flutter)
    - [Using AnimatedContainer](#using-animatedcontainer)
    - [Using AnimatedBuilder](#using-animatedbuilder)
4. [Conclusion](#conclusion)
5. [References](#references)

## What is SVG? {#what-is-svg}
SVG is an open standard format for two-dimensional vector graphics, defined by the World Wide Web Consortium (W3C). It allows us to create and manipulate vector-based graphics that can be scaled without losing quality. SVG files are typically created with vector graphic editors and can be rendered directly or used in web applications.

## SVG Transformations {#svg-transformations}
SVG supports various transformations that can be applied to elements within the SVG file. These transformations include translate, scale, rotate, skew, and matrix transformations. In this blog post, we will focus on translate, rotate, and scale transformations.

### Translate Transform {#translate-transform}
The translate transformation moves an element from its current position. It takes two parameters: `tx` for the horizontal translation and `ty` for the vertical translation. To apply a translate transformation in Flutter, we can use the `Transform.translate` widget.

```dart
Transform.translate(
  offset: Offset(tx, ty),
  child: YourWidget(),
),
```

### Rotate Transform {#rotate-transform}
The rotate transformation rotates an element around a fixed point. It takes one parameter: `angle` for the rotation angle in radians. To apply a rotate transformation in Flutter, we can use the `Transform.rotate` widget.

```dart
Transform.rotate(
  angle: angle,
  child: YourWidget(),
),
```

### Scale Transform {#scale-transform}
The scale transformation scales an element by a factor. It takes two parameters: `scaleX` for the horizontal scale factor and `scaleY` for the vertical scale factor. To apply a scale transformation in Flutter, we can use the `Transform.scale` widget.

```dart
Transform.scale(
  scale: scaleFactor,
  child: YourWidget(),
),
```

## Animating SVG in Flutter {#animating-svg-in-flutter}
In Flutter, we can animate SVG elements using various approaches. Two common methods are using the `AnimatedContainer` widget and the `AnimatedBuilder` widget.

### Using AnimatedContainer {#using-animatedcontainer}
The `AnimatedContainer` widget automatically animates changes in its properties such as size, color, and transformations. By updating the properties within an `AnimatedContainer`, we can create smooth animations for SVG elements.

```dart
AnimatedContainer(
  duration: Duration(seconds: 1),
  transform: Matrix4.translationValues(tx, ty, 0),
  child: YourWidget(),
),
```

### Using AnimatedBuilder {#using-animatedbuilder}
The `AnimatedBuilder` widget provides more control over animation by allowing us to define custom animations using a callback function. We can use this widget to animate SVG transformations by updating the transformation matrix.

```dart
AnimatedBuilder(
  animation: _animationController,
  builder: (BuildContext context, Widget child) {
    return Transform(
      transform: Matrix4.translationValues(tx, ty, 0)
          ..rotateZ(angle)
          ..scale(scaleFactor),
      child: YourWidget(),
    );
  },
),
```

## Conclusion {#conclusion}
In this blog post, we learned how to apply SVG transformations and animations in Flutter using Dart code. We explored translate, rotate, and scale transformations and saw how to animate SVG elements using the `AnimatedContainer` and `AnimatedBuilder` widgets. With these techniques, we can create visually appealing and interactive UI elements in Flutter.

## References {#references}
- [Flutter Documentation](https://flutter.dev/docs)
- [SVG W3C Recommendation](https://www.w3.org/TR/SVG2/)