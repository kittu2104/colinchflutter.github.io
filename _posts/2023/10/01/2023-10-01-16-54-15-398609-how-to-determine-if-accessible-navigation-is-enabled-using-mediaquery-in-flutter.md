---
layout: post
title: "How to determine if accessible navigation is enabled using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [Accessibility]
comments: true
share: true
---

In Flutter, you can use the `MediaQuery` class to determine if accessible navigation is enabled on the device or simulator. Accessible navigation typically refers to features like assistive touch, voice control, or any other accessibility settings that assist users with disabilities in navigating the app.

To determine if accessible navigation is enabled, follow these steps:

1. Import the Flutter material package:

   ```dart
   import 'package:flutter/material.dart';
   ```

2. Use the `MediaQuery` class to access the device's media information. This class provides a way to gather information about the current device and its settings.

3. Retrieve the instance of `MediaQueryData` using `MediaQuery.of` method. This gives you access to the media information for the current context:

   ```dart
   MediaQueryData mediaQuery = MediaQuery.of(context);
   ```

4. Use the `accessibleNavigation` property of MediaQueryData to determine if accessible navigation is enabled. This property returns a boolean value (`true` if accessible navigation is enabled, `false` otherwise):

   ```dart
   bool isAccessibleNavigationEnabled = mediaQuery.accessibleNavigation;
   ```

By following these steps, you can check whether accessible navigation is enabled on the device or simulator in Flutter. This information can be used to adapt the user interface or provide alternative navigation options based on the accessibility settings.

Remember to test your app on devices or simulators with different accessibility settings to ensure a smooth and inclusive user experience.

# Flutter #Accessibility