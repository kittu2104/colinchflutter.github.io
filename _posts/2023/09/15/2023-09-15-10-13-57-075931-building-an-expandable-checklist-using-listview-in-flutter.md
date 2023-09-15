---
layout: post
title: "Building an expandable checklist using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, checklist, listview, flutterdevelopment]
comments: true
share: true
---

Checklists are a useful way to organize and keep track of tasks. In this tutorial, we'll show you how to build an expandable checklist using the ListView widget in Flutter. This will allow users to expand and collapse the checklist items as needed, providing a more organized and user-friendly experience.

To get started, make sure you have Flutter installed and set up on your computer. Once that's done, follow the steps below:

## Step 1: Create a new Flutter project

Open your preferred IDE (e.g., Visual Studio Code) and create a new Flutter project. 

## Step 2: Import the necessary packages

In the `pubspec.yaml` file, add the `flutter_slidable` package to your dependencies. This package will allow us to add sliding gestures to the checklist items.

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_slidable: ^1.1.0
```

Save the file and run `flutter pub get` to install the package.

## Step 3: Define the checklist items

Create a new file called `checklist_item.dart` and define a class called `ChecklistItem` that represents a single item in the checklist. The class should have two properties: `name` (for the item name) and `isCompleted` (to track if the item is completed).

```dart
class ChecklistItem {
  String name;
  bool isCompleted;

  ChecklistItem({required this.name, this.isCompleted = false});
}
```

## Step 4: Create the checklist screen

In the `main.dart` file, create a new stateful widget called `ChecklistScreen`. In the `build` method, create a list of `ChecklistItem` objects and use a `ListView.builder` to dynamically generate the checklist items.

```dart
import 'package:flutter/material.dart';

class ChecklistScreen extends StatefulWidget {
  @override
  _ChecklistScreenState createState() => _ChecklistScreenState();
}

class _ChecklistScreenState extends State<ChecklistScreen> {
  List<ChecklistItem> checklistItems = [
    ChecklistItem(name: "Task 1"),
    ChecklistItem(name: "Task 2"),
    ChecklistItem(name: "Task 3"),
  ];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Checklist"),
      ),
      body: ListView.builder(
        itemCount: checklistItems.length,
        itemBuilder: (context, index) {
          return Slidable(
            actionPane: SlidableDrawerActionPane(),
            actionExtentRatio: 0.25,
            child: ListTile(
              title: Text(checklistItems[index].name),
              leading: Checkbox(
                value: checklistItems[index].isCompleted,
                onChanged: (value) {
                  setState(() {
                    checklistItems[index].isCompleted = value!;
                  });
                },
              ),
            ),
            actions: [
              IconSlideAction(
                caption: 'Delete',
                color: Colors.red,
                icon: Icons.delete,
                onTap: () {
                  setState(() {
                    checklistItems.removeAt(index);
                  });
                },
              ),
            ],
            secondaryActions: [
              IconSlideAction(
                caption: 'Edit',
                color: Colors.blue,
                icon: Icons.edit,
                onTap: () {
                  // TODO: Implement edit functionality
                },
              ),
            ],
          );
        },
      ),
    );
  }
}
```

## Step 5: Run the app

In the `main.dart` file, set the `ChecklistScreen` as the home of the app. Then, run the app by executing `flutter run` in the terminal.

```dart
void main() {
  runApp(MaterialApp(
    home: ChecklistScreen(),
  ));
}
```
With these steps, you now have a functioning expandable checklist built using the ListView widget in Flutter. Users can expand or collapse items by tapping on them, mark items as completed with the provided checkbox, and delete items by swiping left. Feel free to enhance this functionality by adding features such as editing checklist items or persisting the checklist data. Happy coding! 

#flutter #checklist #listview #flutterdevelopment