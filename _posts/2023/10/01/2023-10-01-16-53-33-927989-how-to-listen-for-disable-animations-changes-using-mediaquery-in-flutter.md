---
layout: post
title: "How to listen for disable animations changes using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [flutter, animation]
comments: true
share: true
---

Animations are a vital part of modern app development as they enhance user experience by providing interactive and engaging interfaces. However, sometimes users may prefer to disable animations for various reasons, such as conserving battery life or reducing motion sickness. As a Flutter developer, it is important to be able to listen for changes in the animation settings of the device so that you can adjust your app accordingly.

One way to achieve this is by using MediaQuery, a Flutter widget that provides information about the current device's screen, pixel density, and much more. MediaQuery allows us to access the current animation setting and listen for any changes. Here's how you can do it:

## Step 1: Import the necessary packages

First, you need to import the necessary packages in your Flutter project. Add the following import statement at the beginning of the Dart file:

```dart
import 'package:flutter/services.dart';
```

## Step 2: Define a listener function

Next, define a listener function that will be triggered whenever there is a change in the animation settings. This function will be responsible for handling the appropriate actions based on the animation enable/disable status. For example, you might want to update your app's UI or adjust the speed of your animations. Here's an example of a listener function:

```dart
void _animationSettingsChanged(bool animationsEnabled) {
    if (animationsEnabled) {
        // Enable animations
        // Perform necessary actions
    } else {
        // Disable animations
        // Perform necessary actions
    }
}
```

## Step 3: Add the listener to MediaQuery

Now, you can add the listener function to MediaQuery using the `addOverride` method. This method allows you to override the default values provided by MediaQuery and execute custom logic when the animation setting changes. Here's an example of how to add the listener:

```dart
@override
Widget build(BuildContext context) {
    MediaQueryData mediaQueryData = MediaQuery.of(context);
    mediaQueryData = mediaQueryData.copyWith(
        disableAnimations: false, // default animation state
    );
    mediaQueryData = mediaQueryData.addOverride(
        MediaQueryData.fromWindow(WidgetsBinding.instance.window),
    );
    WidgetsBinding.instance.addPostFrameCallback(
        (Duration timeStamp) {
            // Listen for changes in the animation settings
            _animationSettingsChanged(
                !mediaQueryData.disableAnimations,
            );
        },
    );
    return MaterialApp(
        ...
    );
}
```

## Step 4: Implement the necessary code

Finally, you need to implement the necessary code within the listener function to handle the animation enable/disable status. This might involve updating the UI, adjusting animation speeds, or any other logic specific to your app. Remember to test your app thoroughly to ensure that it behaves as expected when the animation settings are changed.

By listening for changes in the animation settings using MediaQuery, you can ensure that your Flutter app is adaptive and provides a seamless user experience for all users, regardless of their animation preferences.

#flutter #animation