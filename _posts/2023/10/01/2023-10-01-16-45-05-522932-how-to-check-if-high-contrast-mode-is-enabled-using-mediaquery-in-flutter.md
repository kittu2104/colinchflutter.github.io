---
layout: post
title: "How to check if high contrast mode is enabled using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [accessibility]
comments: true
share: true
---

Flutter provides a MediaQuery class that allows you to retrieve information about the accessibility settings on the device. One important setting that you may need to check is whether high contrast mode is enabled. High contrast mode is a setting that adjusts the colors and contrast to make content more readable for visually impaired users. Here's how you can check if high contrast mode is enabled using MediaQuery in Flutter:

1. Get the current MediaQuery data using `MediaQuery.of(context)`.

```dart
MediaQueryData mediaQueryData = MediaQuery.of(context);
```

2. Use the `mediaQueryData` object to check if high contrast mode is enabled. 

```dart
bool isHighContrastEnabled = mediaQueryData.highContrast;
```

The `highContrast` property of the `MediaQueryData` class returns a boolean value indicating whether high contrast mode is enabled or not.

3. Use the `isHighContrastEnabled` variable to conditionally change the UI based on the high contrast mode status.

```dart
if (isHighContrastEnabled) {
  // Apply special UI styling for high contrast mode
} else {
  // Use default UI styling
}
```

By checking the status of the `highContrast` property, you can adapt your UI to accommodate users who have enabled high contrast mode on their device.

Remember to handle this check appropriately in your application to provide an inclusive experience for all users.

#flutter #accessibility