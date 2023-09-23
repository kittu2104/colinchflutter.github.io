---
layout: post
title: "Screen recording and screenshots extensions for Flutter"
description: " "
date: 2023-09-23
tags: [flutter, flutterextensions]
comments: true
share: true
---

If you're developing a Flutter app, you might need to include screen recording or screenshot functionality. Fortunately, there are several extensions available that make it easy to implement these features into your Flutter projects. In this blog post, we will explore two popular extensions: `flutter_screen_recording` and `screenshot`.

## 1. flutter_screen_recording

The `flutter_screen_recording` extension allows you to capture the screen of your Flutter app as a video. This can be useful for creating demo videos, bug reporting, or any other scenario where you need to record the app's behavior. To use this extension, follow these steps:

1. Add the `flutter_screen_recording` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_screen_recording: ^0.2.1
```

2. Import the package into your Dart file:

```dart
import 'package:flutter_screen_recording/flutter_screen_recording.dart';
```

3. Use the `startRecordScreen` method to begin the screen recording:

```dart
await FlutterScreenRecording.startRecordScreen("Your video name");
```

4. To stop the recording, use the `stopRecordScreen` method:

```dart
String filePath = await FlutterScreenRecording.stopRecordScreen;
```

The recorded video will be saved at the specified file path, which you can use as needed within your app.

## 2. screenshot

The `screenshot` extension enables you to capture screenshots of your Flutter app. This can be useful for generating app previews or capturing specific screens for documentation purposes. Follow these steps to integrate `screenshot` into your Flutter project:

1. Add the `screenshot` package to your `pubspec.yaml` file:

```yaml
dependencies:
  screenshot: ^0.3.0
```

2. Import the package into your Dart file:

```dart
import 'package:screenshot/screenshot.dart';
```

3. Create an instance of the `ScreenshotController`:

```dart
ScreenshotController screenshotController = ScreenshotController();
```

4. Wrap the desired widget with the `Screenshot` widget:

```dart
Screenshot(
  controller: screenshotController,
  child: // Your widget here,
);
```

5. To capture a screenshot, call the `capture` method:

```dart
screenshotController.capture().then((image) {
  // Process the captured image as needed
});
```

The `image` variable will contain the captured image, which you can utilize within your app.

These extensions will add valuable functionality to your Flutter app, allowing you to record the screen or capture screenshots effortlessly. Remember to import the necessary dependencies, follow the provided code examples, and tailor the functionalities to your specific use cases.

#flutter #flutterextensions