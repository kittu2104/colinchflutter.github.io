---
layout: post
title: "Using SVG to create dynamic and interactive timelines in Flutter"
description: " "
date: 2023-10-31
tags: []
comments: true
share: true
---

In this blog post, we will explore how to use Scalable Vector Graphics (SVG) to create dynamic and interactive timelines in Flutter. Timelines are a common UI component used to showcase a sequence of events or steps in a specified order. With SVG, we can easily manipulate and animate the timeline elements, providing a rich user experience.

## What is SVG?

SVG is an XML-based vector image format that allows us to create and manipulate images using code. It is widely supported by modern web browsers and can also be used within Flutter to create custom graphics and animations.

## Setting Up the Project

To get started, create a new Flutter project and import the `flutter_svg` package by adding it to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_svg: ^0.22.0
```

Next, run `flutter pub get` to fetch the package and its dependencies.

## Creating the Timeline

To create a timeline, we'll start by defining the structure and appearance using SVG XML code. Here's an example of a simple timeline SVG:

```xml
<svg xmlns="http://www.w3.org/2000/svg" width="400" height="200">
  <line x1="50" y1="100" x2="350" y2="100" stroke="black" stroke-width="2" />
  
  <circle cx="50" cy="100" r="10" fill="black" />
  <circle cx="200" cy="100" r="10" fill="black" />
  <circle cx="350" cy="100" r="10" fill="black" />
</svg>
```

This SVG code creates a horizontal line with three circles representing points on the timeline. The `cx` and `cy` attributes of the circles define their center coordinates, and the `r` attribute sets their radius. The `stroke` and `stroke-width` attributes specify the style of the line.

## Integrating SVG in Flutter

Now that we have our SVG code, we can integrate it into our Flutter project using the `SvgPicture` widget provided by the `flutter_svg` package. First, add the following import statement to the file where you want to use the SVG:

```dart
import 'package:flutter_svg/flutter_svg.dart';
```

Next, create a widget that wraps the `SvgPicture` and provides the SVG code as the source:

```dart
SvgPicture.asset(
  'assets/timeline.svg',
  width: 400,
  height: 200,
),
```

Make sure to place your SVG file in the `assets` folder of your Flutter project. In the example above, we assume that the SVG file is named `timeline.svg`. Adjust the width and height properties as needed to fit your layout.

## Adding Interaction and Animation

To make the timeline interactive, we can attach gesture detection to the circles in the SVG. For example, we can listen for taps on a circle and animate its color change. 

Here's an example of how to handle a tap on a circle and animate its color change using the `flutter_svg` package and Flutter's `GestureDetector` widget:

```dart
GestureDetector(
  onTap: () {
    setState(() {
      circleColor = Colors.blue;
    });
  },
  child: CircleAvatar(
    backgroundColor: circleColor,
    radius: 10,
  ),
),
```

By wrapping the circle with a `GestureDetector` widget, we can listen to various touch events and perform actions accordingly. In this example, we change the `backgroundColor` of the circle to blue when it is tapped.

You can apply similar logic to other gestures like swiping or long-pressing to create more interactive timelines.

## Conclusion

With SVG and Flutter, we can create dynamic and interactive timelines that enhance the user experience of our applications. We learned how to integrate SVG code into Flutter using the `flutter_svg` package and how to add interactivity and animation to our timeline elements. Feel free to explore more advanced SVG features to create even more engaging timelines.

#flutter #SVG