---
layout: post
title: "Drawing emoji art in Flutter"
description: " "
date: 2023-10-04
tags: [setting, drawing]
comments: true
share: true
---

Flutter is a popular cross-platform framework for building mobile applications. It simplifies the process of creating visually appealing user interfaces. With Flutter, you can also draw emoji art to create a fun and engaging user experience. In this tutorial, we will explore how to draw emoji art in a Flutter app.

## Table of Contents
- [Setting Up a Flutter Project](#setting-up-a-flutter-project)
- [Drawing Emoji Art](#drawing-emoji-art)
- [Conclusion](#conclusion)

## Setting Up a Flutter Project

Before diving into drawing emoji art, let's set up a Flutter project to work with. Follow the steps below:

1. Install Flutter on your machine by following the official [installation guide](https://flutter.dev/docs/get-started/install).

2. Create a new Flutter project using the following command:

```dart
flutter create emoji_art_flutter
```

3. Navigate to the project directory:

```dart
cd emoji_art_flutter
```

4. Open the project in your favorite code editor.

## Drawing Emoji Art

Now that we have our Flutter project set up, let's start drawing some emoji art. Follow the steps below to get started:

1. Open the `lib/main.dart` file in your project.

2. Import the `flutter_svg` package to work with SVG images. Add the following line at the beginning of the file:

```dart
import 'package:flutter_svg/flutter_svg.dart';
```

3. Inside the `build` method of the `MyApp` class, create a new `Container` widget and set its `width` and `height` to a specific size. This will be the canvas on which we will draw the emoji art.

```dart
Container(
  width: 300,
  height: 300,
  child: // Emoji art goes here
)
```

4. Now, we can draw the emoji art using SVG images. Download or find a suitable SVG file of an emoji art that you want to display. Place the SVG file in the project directory, for example, `assets/emoji_art.svg`.

5. Add the following code inside the `child` property of the `Container` widget:

```dart
child: SvgPicture.asset('assets/emoji_art.svg'),
```

Make sure to replace `'assets/emoji_art.svg'` with the path to your SVG file.

6. Run the app and see the emoji art displayed on the screen:

```dart
flutter run
```

Congratulations! You have successfully drawn emoji art in your Flutter app.

## Conclusion

In this tutorial, we learned how to draw emoji art using SVG images in a Flutter app. Flutter provides powerful tools for creating engaging user interfaces, and with the help of SVG, we can easily incorporate emoji art into our applications. Get creative and experiment with different emoji art designs to make your app more fun and visually appealing.

#flutter #emojiart