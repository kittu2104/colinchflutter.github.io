---
layout: post
title: "Implementing routing and navigation in Flutter SSR"
description: " "
date: 2023-09-21
tags: [FlutterSSR, RoutingInFlutterSSR]
comments: true
share: true
---

Flutter Server Side Rendering (SSR) is a powerful framework that allows developers to build web applications using Flutter. One essential aspect of building web applications is implementing routing and navigation to enable users to navigate between different pages of the application. In this blog post, we will explore how to implement routing and navigation in Flutter SSR.

## Setting Up Flutter SSR Project

Before we dive into routing and navigation, let's start by setting up a Flutter SSR project. Here are the steps to get started:

1. Install Flutter and set up your development environment.
2. Create a new Flutter project:

```dart
flutter create flutter_ssr_project
cd flutter_ssr_project
```

3. Add `flutter_ssr` as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_ssr: ^x.x.x
```

4. Run `flutter pub get` to fetch the dependency.

## Implementing Routing in Flutter SSR

To implement routing in Flutter SSR, follow these steps:

1. Create a `routes.dart` file in your project's `lib` folder. This file will contain all the routes for your application.

2. Import the necessary Flutter packages:

```dart
import 'package:flutter_ssr/flutter_ssr.dart';
import 'package:universal_html/prefer_universal/html.dart' as html;
```

3. Define a `Map` where the keys represent the route paths and the values represent the corresponding widget to be shown:

```dart
final Map<String, Widget Function(HtmlParams queryParams)> routes = {
  '/': (queryParams) => HomePage(),
  '/about': (queryParams) => AboutPage(),
  '/contact': (queryParams) => ContactPage(),
};
```

4. Create a `Router` widget that uses the `RouteHandler` from `flutter_ssr` package to handle the routing logic:

```dart
class Router extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return RouteHandler(
      initialPath: html.window.location.pathname,
      routes: routes,
      pageBuilder: (child) => MaterialApp(
        title: 'Flutter SSR Routing',
        home: child,
      ),
    );
  }
}
```

5. Finally, add the `Router` widget to your `main.dart` file:

```dart
void main() {
  runApp(Router());
}
```

## Navigating Between Pages

Now that we have implemented routing, let's see how we can navigate between different pages in our Flutter SSR application.

To navigate to a specific page, use the following code:

```dart
html.window.history.pushState(null, 'Page Title', '/about');
```

This will change the URL and trigger the routing logic to load the corresponding page component.

To add navigation links in your application, you can use the `html.AnchorElement` from the `universal_html` package:

```dart
html.AnchorElement()
  ..text = 'About'
  ..href = '/about'
  ..style.setProperty('margin-right', '10px')
  ..style.setProperty('cursor', 'pointer')
  ..onClick.listen((_) {
    html.window.history.pushState(null, 'About', '/about');
  })
  ..appendTo(html.document.body);
```

This code will create an `<a>` tag with the text 'About' and a click listener that triggers the navigation.

That's it! You have successfully implemented routing and navigation in your Flutter SSR project.

#FlutterSSR #RoutingInFlutterSSR