---
layout: post
title: "Implementing drag-to-dismiss functionality in ListView in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, FlutterTutorial]
comments: true
share: true
---

When designing mobile apps, it's important to provide a seamless user experience. One way to enhance the user experience is by implementing drag-to-dismiss functionality in ListView. This allows users to easily swipe away or dismiss items in a list.

In this tutorial, we will explore how to implement drag-to-dismiss functionality in ListView using Flutter, a popular cross-platform framework for building mobile apps.

## Prerequisites

Make sure you have Flutter installed on your machine. If not, you can follow the official Flutter installation guide for your operating system.

## Step 1: Set up a Flutter project

Create a new Flutter project by running the following command in your terminal:

```dart
flutter create drag_to_dismiss_example
```

## Step 2: Adding dependencies

Open the `pubspec.yaml` file in your project directory and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_slidable: ^0.6.0
```

Save the file and run the following command to fetch the dependencies:

```dart
flutter pub get
```

## Step 3: Building the ListView

Open the `lib/main.dart` file in your project directory and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_slidable/flutter_slidable.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final List<String> items = List.generate(20, (index) => 'Item ${index + 1}');

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Drag to Dismiss ListView'),
        ),
        body: ListView.builder(
          itemCount: items.length,
          itemBuilder: (context, index) {
            final item = items[index];
            return Slidable(
              actionPane: SlidableDrawerActionPane(),
              secondaryActions: [
                IconSlideAction(
                  caption: 'Delete',
                  color: Colors.red,
                  icon: Icons.delete,
                  onTap: () {
                    // Handle delete action
                    _removeItem(index);
                  },
                ),
              ],
              child: ListTile(
                title: Text(item),
              ),
            );
          },
        ),
      ),
    );
  }

  void _removeItem(int index) {
    // Remove item from the list
    items.removeAt(index);
  }
}
```

This code sets up a basic Flutter application with a ListView that generates 20 items. We are using the `flutter_slidable` package to enable drag-to-dismiss functionality. The `Slidable` widget wraps each `ListTile` in the ListView and provides the swipe actions.

## Step 4: Running the app

Save the changes and run the app using the following command:

```dart
flutter run
```

You should now see the app running on the device or emulator, displaying a ListView with 20 items. Swipe left on any item to reveal the delete action and drag it further to dismiss the item.

Congratulations! You have successfully implemented drag-to-dismiss functionality in ListView in Flutter. Try customizing the swipe actions and explore more features of the `flutter_slidable` package to enhance your app's user experience.

#flutter #FlutterTutorial