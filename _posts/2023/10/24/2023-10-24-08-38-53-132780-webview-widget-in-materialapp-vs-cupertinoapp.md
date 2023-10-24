---
layout: post
title: "Webview widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [webview]
comments: true
share: true
---

When it comes to developing cross-platform apps with Flutter, you have the option to choose between using the `MaterialApp` or `CupertinoApp` widget as the root widget for your app. These widgets provide different design styles based on the platform they are running on - Material Design for Android and iOS-like design for iOS.

One common requirement in many apps is to display web content within the app. Flutter provides the `webview_flutter` package, which allows you to embed a webview within your app. However, there are some differences in using the `webview_flutter` package with `MaterialApp` and `CupertinoApp`. Let's take a closer look at them.

## Using `webview_flutter` with MaterialApp

When using the `webview_flutter` package with the `MaterialApp` widget, you can make use of the `WebView` widget provided by the package. This widget gives you the freedom to customize the look and feel of the webview using the rich set of Material Design components.

Here's an example of using `WebView` within a `MaterialApp`:

```dart
import 'package:flutter/material.dart';
import 'package:webview_flutter/webview_flutter.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Webview in MaterialApp'),
      ),
      body: WebView(
        initialUrl: 'https://example.com',
        javascriptMode: JavascriptMode.unrestricted,
      ),
    ),
  ));
}
```

The above code sets up a basic Flutter app with a `MaterialApp` as the root widget. The `WebView` widget is used as the body of the `Scaffold` widget, allowing web content to be displayed within the app.

## Using `webview_flutter` with CupertinoApp

Similarly, you can also use the `webview_flutter` package with the `CupertinoApp` widget. However, since `CupertinoApp` follows iOS design guidelines, the `WebView` widget provided by the package will adopt an iOS-like appearance.

Here's an example of using `WebView` within a `CupertinoApp`:

```dart
import 'package:flutter/cupertino.dart';
import 'package:webview_flutter/webview_flutter.dart';

void main() {
  runApp(CupertinoApp(
    home: CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Webview in CupertinoApp'),
      ),
      child: WebView(
        initialUrl: 'https://example.com',
        javascriptMode: JavascriptMode.unrestricted,
      ),
    ),
  ));
}
```

In this code snippet, we set up a basic Flutter app with a `CupertinoApp` as the root widget. The `WebView` widget is used as the child of the `CupertinoPageScaffold`. The navigation bar at the top follows iOS design guidelines, providing a consistent user experience.

## Conclusion

The choice between using `MaterialApp` or `CupertinoApp` with the `webview_flutter` package ultimately depends on the desired design style for your app. If you prefer a Material Design look and feel, go with `MaterialApp`. If you want the app to have an iOS-like appearance, choose `CupertinoApp`.

Remember to import the `webview_flutter` package and follow the installation instructions before using the `WebView` widget in your Flutter project.

#flutter #webview