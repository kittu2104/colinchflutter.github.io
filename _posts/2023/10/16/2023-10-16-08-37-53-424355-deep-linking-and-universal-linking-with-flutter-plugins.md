---
layout: post
title: "Deep linking and universal linking with Flutter plugins"
description: " "
date: 2023-10-16
tags: [references]
comments: true
share: true
---

In this blog post, we will explore how to implement deep linking and universal linking in your Flutter app using plugins. Deep linking and universal linking allow users to navigate to specific content or perform specific actions within an app, directly from a URL.

## Table of Contents
- [What is Deep Linking?](#what-is-deep-linking)
- [What is Universal Linking?](#what-is-universal-linking)
- [Implementing Deep Linking with Flutter Plugins](#implementing-deep-linking-with-flutter-plugins)
- [Implementing Universal Linking with Flutter Plugins](#implementing-universal-linking-with-flutter-plugins)
- [Conclusion](#conclusion)

## What is Deep Linking?

Deep linking is the practice of using a URL to launch a specific screen or perform a specific action within an app. It allows users to seamlessly navigate to a specific location within an app without having to navigate through multiple screens manually.

For example, an e-commerce app can use deep linking to direct users to a specific product page when they click on a link shared via email or social media. Deep linking enhances user experience by providing a seamless transition from a website or other apps to an app.

## What is Universal Linking?

Universal linking is similar to deep linking but is specific to iOS devices. It allows iOS apps to handle HTTP and HTTPS links, enabling navigation to specific app content through a web URL. When a user clicks on a universal link, iOS will check if the corresponding app is installed and then launch the app directly to the specified content.

The advantage of universal linking is that it provides a consistent user experience across different platforms and allows the app to handle links clicked within the device's browser or other apps.

## Implementing Deep Linking with Flutter Plugins

To implement deep linking in your Flutter app, you can use plugins like `url_launcher` and `flutter_deeplink`. 

The `url_launcher` plugin allows you to launch URLs externally, while the `flutter_deeplink` plugin provides a more extensive API for handling deep links within your app.

Here's an example of how to use `url_launcher` to open a URL:

```dart
import 'package:url_launcher/url_launcher.dart';

void _launchURL() async {
  const url = 'https://example.com';
  if (await canLaunch(url)) {
    await launch(url);
  } else {
    throw 'Could not launch $url';
  }
}
```

To handle deep links within your app, you can use the `flutter_deeplink` plugin. It allows you to define routes based on different URIs and handle them accordingly. Here's an example of using `flutter_deeplink`:

```dart
import 'package:flutter_deeplink/flutter_deeplink.dart';

void main() {
  runApp(MyApp());
  final router = DeeplinkRouter(
    routes: {
      '/product/:id': (Map<String, String> parameters) {
        final productId = parameters['id'];
        // Perform actions based on the productId
      },
      '/cart': (_) {
        // Navigate to the cart screen
      },
    },
  );
  router.run();
}
```

## Implementing Universal Linking with Flutter Plugins

To implement universal linking in your Flutter app specifically for iOS, you can use the `flutter_udid` plugin. This plugin enables handling of universal links and provides callbacks to handle the deeplink URL.

To use `flutter_udid`, add it as a dependency in your `pubspec.yaml` file. Then, in your `AppDelegate.swift` file, you can add the following code to handle the universal link:

```swift
import UIKit
import Flutter
import flutter_udid

@UIApplicationMain
class AppDelegate: FlutterAppDelegate {
  override func application(
    _ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
  ) -> Bool {
    GeneratedPluginRegistrant.register(with: self)
    
    // Handling universal links
    FlutterUdidPlugin.handleUniversalLink(launchOptions)
    
    return super.application(application, didFinishLaunchingWithOptions: launchOptions)
  }
  
  // Callback for handling the universal link
  override func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
      if FlutterUdidPlugin.isUniversalLink(url) {
          FlutterUdidPlugin.handleUniversalLink(url)
          return true
      }
      return false
  }
}
```

## Conclusion

Deep linking and universal linking are powerful techniques to improve user experience and drive engagement in your Flutter app. By implementing these features using the appropriate Flutter plugins, you can seamlessly navigate users to specific screens or perform actions within your app directly from URLs.

Remember to make use of plugins like `url_launcher`, `flutter_deeplink`, and `flutter_udid` to simplify the implementation process and handle deep links and universal links effectively.

#references 637d0f43