---
layout: post
title: "Using webviews in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In this article, we will explore how to integrate webviews into a Flutter application built using the `MaterialApp` widget. Webviews are powerful tools that allow you to display web content within your application, enabling you to create hybrid apps or integrate web features into your native app.

## Table of Contents
- [Setting up the dependencies](#setting-up-the-dependencies)
- [Creating the webview widget](#creating-the-webview-widget)
- [Navigating with webviews](#navigating-with-webviews)
- [Handling webview events](#handling-webview-events)
- [Conclusion](#conclusion)

## Setting up the dependencies
To use webviews in a Flutter app, you need to include the `webview_flutter` package in your `pubspec.yaml` file. Add the following line to the `dependencies` section:

```yaml
dependencies:
  webview_flutter: ^2.0.10
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Creating the webview widget
In this example, we will create a `WebView` widget wrapped in a `Scaffold` within a `MaterialApp`. The `WebView` widget is responsible for loading and displaying web content.

```dart
import 'package:flutter/material.dart';
import 'package:webview_flutter/webview_flutter.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Webview Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Webview Demo'),
        ),
        body: WebView(
          initialUrl: 'https://example.com',
          javascriptMode: JavascriptMode.unrestricted,
        ),
      ),
    );
  }
}
```

In the above code snippet, we import the necessary packages and define a `MyApp` widget. Inside the `build()` method, we return a `MaterialApp` widget, which is wrapped in a `Scaffold` widget to provide a material design layout. The `WebView` widget is placed inside the `body` property of the `Scaffold` and is configured with the initial URL and `JavascriptMode`.

## Navigating with webviews
Webviews allow users to navigate between different web pages within your app. To enable navigation, you can use the `WebView` widget's `navigationDelegate` property. 

```dart
WebView(
  initialUrl: 'https://example.com',
  javascriptMode: JavascriptMode.unrestricted,
  navigationDelegate: (NavigationRequest request) {
    if (request.url.startsWith('https://example.com')) {
      return NavigationDecision.navigate;
    }
    return NavigationDecision.prevent;
  },
)
```

The `navigationDelegate` takes a `NavigationRequest` parameter. You can check the URL of the requested page and decide whether to allow the navigation or prevent it.

## Handling webview events
Webviews provide event listeners to handle events such as page loads and error events. You can use these event listeners to enhance the user experience and handle specific scenarios.

```dart
WebView(
  // ...
  onPageStarted: (String url) {
    print('Page started loading: $url');
  },
  onPageFinished: (String url) {
    print('Page finished loading: $url');
  },
  onWebResourceError: (WebResourceError error) {
    print('Web resource error: $error');
  },
)
```

In the example above, we have added event listeners for `onPageStarted`, which prints the URL of the starting page, `onPageFinished`, which prints the URL of the finished page, and `onWebResourceError`, which prints any encountered errors.

## Conclusion
Integrating webviews into your Flutter app using the `MaterialApp` widget is a straightforward process. By following the steps outlined in this article, you can easily display web content and enable navigation within your app. Webviews offer a powerful way to combine web and native features, providing a seamless user experience.

Remember to check out the official `webview_flutter` package documentation for more advanced usage and customization options.

# Hashtags:
TechBlog #Flutter