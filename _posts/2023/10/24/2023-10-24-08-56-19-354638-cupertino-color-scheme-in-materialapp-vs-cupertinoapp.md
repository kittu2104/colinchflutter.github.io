---
layout: post
title: "Cupertino color scheme in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [mobile]
comments: true
share: true
---

When developing a Flutter application, you have the choice of using either the `MaterialApp` or `CupertinoApp` widget as the root of your widget tree. These widgets provide different design systems and UI components, with the `MaterialApp` following Material Design principles and the `CupertinoApp` following the Cupertino design language.

One key difference between the two is the color scheme used. Material Design uses a vibrant color palette, while Cupertino design primarily uses gray-scale colors. This distinction is important to consider when deciding which widget to use for your app.

Let's take a closer look at how the color scheme differs between `MaterialApp` and `CupertinoApp`.

## MaterialApp Color Scheme

By default, the `MaterialApp` widget uses the Material Design color scheme. This means that it uses vibrant colors, such as primary and accent colors, to visually distinguish different parts of the UI. These colors can be customized using the `theme` property of the `MaterialApp` widget.

Here is an example of defining a custom color scheme for a `MaterialApp`:

```dart
MaterialApp(
  theme: ThemeData(
    primaryColor: Colors.blue,
    accentColor: Colors.orange,
  ),
  // rest of the code
)
```

In this example, the `primaryColor` is set to blue, and the `accentColor` is set to orange. These colors will be used throughout the app to provide a cohesive visual experience.

## CupertinoApp Color Scheme

On the other hand, the `CupertinoApp` widget uses the Cupertino design language, which emphasizes a gray-scale color palette. The default color scheme of the Cupertino design language is more subdued and minimalistic compared to Material Design.

To customize the color scheme in a `CupertinoApp`, you can use the `theme` property of the `CupertinoApp` widget:

```dart
CupertinoApp(
  theme: CupertinoThemeData(
    primaryColor: CupertinoColors.activeBlue,
    scaffoldBackgroundColor: CupertinoColors.white,
  ),
  // rest of the code
)
```

In this example, the `primaryColor` is set to activeBlue, and the `scaffoldBackgroundColor` is set to white. These colors will be used throughout the app to maintain the consistent Cupertino appearance.

## Choosing Between MaterialApp and CupertinoApp

When deciding whether to use `MaterialApp` or `CupertinoApp`, you should consider the design language you want to follow and choose the widget that aligns with your desired visual style. If your app needs to follow Material Design guidelines and use the vibrant Material Design color scheme, go with `MaterialApp`. If you want a more subdued and gray-scale color scheme that matches the Cupertino design language, `CupertinoApp` is the right choice.

Remember, you can still override the default color schemes for both widgets to create a custom look and feel that is consistent with your app's branding.

To summarize, the color schemes in `MaterialApp` and `CupertinoApp` differ due to the design languages they follow. It's essential to choose the appropriate widget based on the visual style and color scheme requirements of your app.

**#flutter #mobile**