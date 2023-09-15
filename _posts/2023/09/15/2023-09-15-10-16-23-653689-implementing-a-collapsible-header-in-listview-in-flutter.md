---
layout: post
title: "Implementing a collapsible header in ListView in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, collapsibleheader]
comments: true
share: true
---

In this tutorial, we will explore how to implement a collapsible header in a ListView in Flutter. A collapsible header provides an interactive way for users to expand or collapse a section of content within a ListView.

Let's get started!

## Prerequisites

Before proceeding, make sure you have Flutter installed on your machine. If not, head over to the [Flutter website](https://flutter.dev/) and follow the installation instructions.

## Step 1: Create a new Flutter project

To create a new Flutter project, open your terminal or command prompt and run the following command:

```bash
flutter create collapsible_header
```

This will create a new project named `collapsible_header`.

## Step 2: Update the `pubspec.yaml` file

Inside the `pubspec.yaml` file, add the `flutter_slidable` dependency under the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_slidable: ^0.6.0
```

Save the file and run the following command to fetch the dependencies:

```bash
flutter pub get
```

## Step 3: Update the `main.dart` file

Open the `main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_slidable/flutter_slidable.dart';

void main() {
  runApp(CollapsibleHeaderApp());
}

class CollapsibleHeaderApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Collapsible Header',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: CollapsibleHeaderPage(),
    );
  }
}
```

## Step 4: Create the `CollapsibleHeaderPage` widget

In a new file named `collapsible_header_page.dart`, add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_slidable/flutter_slidable.dart';

class CollapsibleHeaderPage extends StatefulWidget {
  @override
  _CollapsibleHeaderPageState createState() => _CollapsibleHeaderPageState();
}

class _CollapsibleHeaderPageState extends State<CollapsibleHeaderPage> {
  bool _isExpanded = false;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Collapsible Header'),
      ),
      body: ListView(
        children: [
          Slidable(
            actionExtentRatio: 0.25,
            actions: [
              IconSlideAction(
                caption: 'Action 1',
                icon: Icons.archive,
                onTap: () => print('Action 1 tapped'),
              ),
              IconSlideAction(
                caption: 'Action 2',
                icon: Icons.delete,
                onTap: () => print('Action 2 tapped'),
              ),
            ],
            child: ListTile(
              title: Text('List Item 1'),
            ),
          ),
          AnimatedContainer(
            duration: Duration(milliseconds: 300),
            height: _isExpanded ? 200 : 0,
            child: Padding(
              padding: const EdgeInsets.all(8.0),
              child: Card(
                child: Center(
                  child: Text(
                    'Additional Content',
                    style: TextStyle(fontSize: 20),
                  ),
                ),
              ),
            ),
          ),
          Slidable(
            actionExtentRatio: 0.25,
            actions: [
              IconSlideAction(
                caption: 'Action 1',
                icon: Icons.archive,
                onTap: () => print('Action 1 tapped'),
              ),
              IconSlideAction(
                caption: 'Action 2',
                icon: Icons.delete,
                onTap: () => print('Action 2 tapped'),
              ),
            ],
            child: ListTile(
              title: Text('List Item 2'),
            ),
          ),
        ],
      ),
    );
  }
}
```

## Step 5: Run the app

Save all the files and run the app by executing the following command:

```bash
flutter run
```

You should now see the app running on your device or simulator with a collapsible header in the ListView.

## Conclusion

In this tutorial, we learned how to implement a collapsible header in a ListView in Flutter. By utilizing the `flutter_slidable` package, we were able to create an interactive and user-friendly user interface.

Feel free to customize the code to fit your specific requirements and explore additional features of the `flutter_slidable` package.

Happy coding! 😃

#flutter #collapsibleheader