---
layout: post
title: "Writing platform-specific code for Android in Flutter."
description: " "
date: 2023-09-17
tags: []
comments: true
share: true
---

When working with Flutter, you have the advantage of being able to write cross-platform code that can run on both iOS and Android. However, there may be certain cases where you need to write platform-specific code to access specific functionality on either platform. In this blog post, we will focus on writing platform-specific code for Android in Flutter.

## Step 1: Declaring the platform channel

To communicate between Flutter and Android, we will use the platform channel. The platform channel allows you to invoke platform-specific APIs using method channels. To declare the platform channel, you need to add the following code to your Flutter project:

```dart
import 'package:flutter/services.dart';

const platform = MethodChannel('your_channel_name');
```

Replace `'your_channel_name'` with a unique identifier for your platform channel.

## Step 2: Invoking platform-specific methods

Once you have declared the platform channel, you can invoke platform-specific methods from your Flutter code. Here's an example of invoking a method on Android:

```dart
try {
  final result = await platform.invokeMethod('your_method_name');
  print('Received result from Android: $result');
} on PlatformException catch (e) {
  print('Error while invoking platform method: ${e.message}');
}
```

Replace `'your_method_name'` with the name of the method you want to invoke on Android. The `invokeMethod` function returns a Future that resolves to the result of the method invocation.

## Step 3: Implementing the platform-specific code on Android

To implement the platform-specific code on Android, you will need to create a new Java class that extends `FlutterFragmentActivity`. Here's an example of how to implement a platform-specific method:

```java
import androidx.annotation.NonNull;
import io.flutter.embedding.android.FlutterFragmentActivity;
import io.flutter.embedding.engine.FlutterEngine;
import io.flutter.plugin.common.MethodChannel;
import io.flutter.plugins.GeneratedPluginRegistrant;

public class MainActivity extends FlutterFragmentActivity {
  private static final String CHANNEL = "your_channel_name";

  @Override
  public void configureFlutterEngine(@NonNull FlutterEngine flutterEngine) {
    super.configureFlutterEngine(flutterEngine);
    GeneratedPluginRegistrant.registerWith(flutterEngine);

    new MethodChannel(flutterEngine.getDartExecutor().getBinaryMessenger(), CHANNEL)
        .setMethodCallHandler((methodCall, result) -> {
          if (methodCall.method.equals("your_method_name")) {
            // Add your platform-specific code here
            result.success("Result from Android");
          } else {
            result.notImplemented();
          }
        });
  }
}
```

Make sure to replace `'your_channel_name'` and `'your_method_name'` with the same identifiers used in your Flutter code.

## Conclusion

Writing platform-specific code for Android in Flutter allows you to access specific Android APIs that are not available in Flutter's cross-platform framework. By using the platform channel and method channels, you can easily communicate between your Flutter code and Android native code.