---
layout: post
title: "MediaQuery physicSize in Flutter"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

When building responsive and device-friendly apps in Flutter, we need to consider the different screen sizes and resolutions of the devices our app will run on. Flutter provides the `MediaQuery` class to obtain information about the device's screen properties, including the `physicalSize` property. In this blog post, we will explore how to use the `physicalSize` property to create adaptive UIs in Flutter.

## What is physicalSize in MediaQuery?

In Flutter, `physicalSize` refers to the physical dimensions of the screen, such as its width and height, measured in physical screen pixels. It represents the actual size of the device's screen, taking into account factors like pixel density, which can vary across devices.

## Accessing physicalSize in Flutter

To access the `physicalSize` property, we can use the `MediaQuery.of(context)` method to obtain the `MediaQueryData` object for the current `BuildContext`. From the `MediaQueryData` object, we can access various screen properties, including `physicalSize`. Here's an example:

```dart
MediaQueryData queryData = MediaQuery.of(context);
Size screenSize = queryData.physicalSize;
double screenWidth = screenSize.width;
double screenHeight = screenSize.height;
```

In the code snippet above, we first obtain the `MediaQueryData` object using `MediaQuery.of(context)`. Then, we extract the `physicalSize` property into a `Size` object which holds the width and height of the screen. Finally, we can access the width and height using the `width` and `height` properties of the `Size` object.

## Practical Use Cases

With the `physicalSize` property, we can design adaptive user interfaces that adjust to different screen sizes. Here are a few use cases where `physicalSize` can be useful:

### Responsive layouts

By accessing the physical size of the screen, we can dynamically adjust the layout of our app based on the available screen space. We can use the `physicalSize` to determine if the device has a smaller or larger screen and adjust the UI accordingly. For example, we can modify the spacing between elements or change the layout to better utilize the available space.

### Image and asset scaling

Using the `physicalSize`, we can dynamically scale images and assets to match the screen's resolution. This ensures that images are rendered crisply on each device, regardless of the pixel density. By adjusting the size of images based on the physical screen size, we can provide a better user experience across different devices.

## Conclusion

Understanding and utilizing the `physicalSize` property of the `MediaQuery` class in Flutter allows us to create responsive and adaptive user interfaces that work seamlessly across different devices. By leveraging the `physicalSize` property, we can build apps that provide a consistent experience, regardless of the screen size and pixel density.