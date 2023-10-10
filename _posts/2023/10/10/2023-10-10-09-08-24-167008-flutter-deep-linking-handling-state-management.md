---
layout: post
title: "Flutter deep linking handling state management"
description: " "
date: 2023-10-10
tags: [DeepLinking]
comments: true
share: true
---

Deep linking is a powerful feature that allows mobile apps to be opened directly from a web link or another app. It provides a seamless user experience by redirecting users to specific screens within an app, while also passing relevant data or parameters.

In this article, we will explore how to handle deep linking and manage the app's state in a Flutter application.

## Table of Contents
- [Introduction to Deep Linking](#introduction-to-deep-linking)
- [Setting Up Deep Linking in Flutter](#setting-up-deep-linking-in-flutter)
- [Handling Deep Links](#handling-deep-links)
- [State Management in Flutter](#state-management-in-flutter)
- [Combining Deep Linking and State Management](#combining-deep-linking-and-state-management)
- [Conclusion](#conclusion)

## Introduction to Deep Linking

Deep linking is the ability to launch a specific screen or view within a mobile app directly from a link. This link can be triggered from a website, another app, or even a push notification. Deep links are typically associated with a specific URL format, such as `myapp://screen1?param1=abc&param2=123`.

## Setting Up Deep Linking in Flutter

To enable deep linking in your Flutter app, you need to add the `url_launcher` and `uni_links` packages to your `pubspec.yaml` file. The `url_launcher` package is responsible for opening the app from a deep link URL, while the `uni_links` package listens for deep link events.

```dart
dependencies:
  url_launcher: ^6.0.1
  uni_links: ^0.5.0
```

After adding the dependencies, run `flutter pub get` to fetch and install the packages.

## Handling Deep Links

To handle deep links in your Flutter app, you need to define a callback function that will be called whenever a deep link is received.

```dart
import 'package:uni_links/uni_links.dart' as uni_links;

void handleDeepLink() async {
  await uni_links.getInitialUri().then((uri) {
    if (uri != null) {
      // Extract and handle the deep link parameters
      // Update the app state based on the deep link parameters
    }
  });

  // Listen for deep link changes
  uni_links.getUriLinksStream().listen((uri) {
    // Extract and handle the deep link parameters
    // Update the app state based on the deep link parameters
  });
}
```

The `handleDeepLink` function retrieves the initial deep link when the app is launched and also listens for changes in deep links while the app is running. Within this function, you can extract the parameters from the deep link URL and update the app state accordingly.

## State Management in Flutter

Flutter offers various state management solutions, such as `setState`, `Provider`, `Bloc`, and `GetX`. These solutions help manage the state of your app and ensure it stays consistent across different screens and widgets.

## Combining Deep Linking and State Management

To handle deep links and manage state in a Flutter app simultaneously, you can use a state management solution like `Provider` or `Bloc`. These state management solutions allow you to update the app state when a deep link is received.

For example, with `Provider`, you can define a `ChangeNotifier` class that holds the app state.

```dart
class AppState extends ChangeNotifier {
  String? deepLinkParam;

  void updateDeepLink(String? param) {
    deepLinkParam = param;
    notifyListeners();
  }
}
```

In your app's main widget, wrap the relevant widgets with a `ChangeNotifierProvider` to provide access to the state.

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (_) => AppState(),
      child: MaterialApp(
        title: 'Flutter Deep Linking State Management',
        home: HomePage(),
      ),
    );
  }
}
```

Finally, update the state when a deep link is received in the `handleDeepLink` function.

```dart
void handleDeepLink() async {
  // ...

  uni_links.getUriLinksStream().listen((uri) {
    // Extract and handle the deep link parameters
    // ...
  
    // Update the app state with the deep link parameter
    Provider.of<AppState>(context, listen: false).updateDeepLink(param);
  });
}
```

By combining deep linking and state management, you can handle deep links while ensuring that the app state reflects the relevant changes.

## Conclusion

In this article, we discussed how to handle deep linking and manage the app's state in a Flutter application. We explored setting up deep linking, handling deep links, and using state management solutions like `Provider` or `Bloc`. By combining deep linking and state management, you can create a seamless user experience in your Flutter app. Remember to update your app's state based on the deep link parameters to provide relevant content to your users.

#hashtags: #Flutter #DeepLinking