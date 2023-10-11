---
layout: post
title: "Implementing lazy loading with dark mode in Flutter"
description: " "
date: 2023-10-11
tags: [adding, conclusion]
comments: true
share: true
---

In this tutorial, we will explore how to implement lazy loading with dark mode in Flutter. Lazy loading is a technique used to load content or resources only when they are needed, which helps improve performance and reduce memory usage. Dark mode, on the other hand, allows users to switch to a darker color scheme, providing a more comfortable viewing experience in low-light environments. 

Let's get started!

## Table of Contents
1. [Setting up the project](#setting-up-the-project)
2. [Implementing lazy loading](#implementing-lazy-loading)
3. [Adding dark mode](#adding-dark-mode)
4. [Conclusion](#conclusion)

## Setting up the project {#setting-up-the-project}

To start, create a new Flutter project by running the following command in your terminal:

```
flutter create lazy_loading_dark_mode
```

Next, navigate to the project directory:

```
cd lazy_loading_dark_mode
```

Open the project in your preferred code editor and let's begin!

## Implementing lazy loading {#implementing-lazy-loading}

Lazy loading in Flutter can be achieved using the `ListView.builder` widget. This widget allows us to build a list of items dynamically as the user scrolls.

First, we'll create a list of items to display. For simplicity, let's assume we have a list of images represented by their URLs.

```dart
List<String> imageUrls = [
  'https://example.com/image1.jpg',
  'https://example.com/image2.jpg',
  'https://example.com/image3.jpg',
  // add more image URLs here
];
```

Next, we'll implement the `ListView.builder` widget to display the images. This widget takes a `itemBuilder` function that is called for each item in the list.

```dart
ListView.builder(
  itemCount: imageUrls.length,
  itemBuilder: (context, index) {
    String imageUrl = imageUrls[index];
    // Load the image lazily using a package like `cached_network_image`
    // Use a placeholder image while the actual image is being loaded
    return Image.network(
      imageUrl,
      fit: BoxFit.cover,
      loadingBuilder: (context, child, loadingProgress) {
        return loadingProgress == null
            ? child
            : CircularProgressIndicator(); // show a loading indicator
      },
    );
  },
);
```

With this implementation, Flutter will only load the images that are currently visible on the screen. As the user scrolls, new images will be loaded on-demand for a smooth and efficient user experience.

## Adding dark mode {#adding-dark-mode}

To add dark mode to our Flutter app, we'll utilize the `provider` package for state management. This package allows us to easily switch between different themes.

First, add the `provider` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.0.0
```

Next, we'll create a `ThemeProvider` class that extends `ChangeNotifier`. This class will hold the current theme data and notify its listeners whenever the theme is changed.

```dart
import 'package:flutter/material.dart';

class ThemeProvider with ChangeNotifier {
  bool _isDarkMode = false;

  bool get isDarkMode => _isDarkMode;

  void toggleDarkMode() {
    _isDarkMode = !_isDarkMode;
    notifyListeners();
  }
}
```

In your app's entry point, wrap your `MaterialApp` with the `ChangeNotifierProvider` to provide the `ThemeProvider` to all its descendants.

```dart
void main() {
  runApp(
    ChangeNotifierProvider(
      create: (_) => ThemeProvider(),
      child: MyApp(),
    ),
  );
}
```

Now, we can use the `ThemeProvider` in our Flutter widgets to toggle between dark and light modes.

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final themeProvider = Provider.of<ThemeProvider>(context);

    return MaterialApp(
      theme: themeProvider.isDarkMode ? ThemeData.dark() : ThemeData.light(),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Lazy Loading with Dark Mode'),
        ),
        body: ListView.builder(
          itemCount: imageUrls.length,
          itemBuilder: (context, index) {
            // Lazy loading implementation
            // ...
          },
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {
            themeProvider.toggleDarkMode();
          },
          child: Icon(Icons.dark_mode),
        ),
      ),
    );
  }
}
```

In this example, we've added a `FloatingActionButton` that toggles the dark mode when pressed. Whenever the dark mode is enabled or disabled, the `ThemeProvider` will notify its listeners, and the app's theme will automatically update.

## Conclusion {#conclusion}

In this tutorial, we've learned how to implement lazy loading with dark mode in Flutter. By utilizing the `ListView.builder` widget, we were able to load content on-demand for improved performance. Additionally, we leveraged the `provider` package to easily implement dark mode and allow users to switch between light and dark themes.

Feel free to customize and enhance this implementation further to suit the needs of your Flutter app. Happy coding!

**#flutter #lazyloading**