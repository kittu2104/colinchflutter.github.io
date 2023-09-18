---
layout: post
title: "Building a todo list app using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [ListView]
comments: true
share: true
---

In this tutorial, we will be building a simple Todo List app using ListView in the Flutter framework. The ListView widget provides an easy way to display a list of items on the screen, making it perfect for creating a todo list.

## Prerequisites

Before we begin, make sure you have Flutter and Dart installed on your machine. You can check if Flutter is installed by running `flutter doctor` in your terminal.

## Step 1: Create a new Flutter project

Open your terminal and run the following command to create a new Flutter project:

```bash
flutter create todo_list
```

## Step 2: Set up the todo_list app

Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(TodoListApp());
}

class TodoListApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Todo List',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: TodoListPage(),
    );
  }
}

class TodoListPage extends StatefulWidget {
  @override
  _TodoListPageState createState() => _TodoListPageState();
}

class _TodoListPageState extends State<TodoListPage> {
  List<String> todos = [];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Todo List'),
      ),
      body: ListView.builder(
        itemCount: todos.length,
        itemBuilder: (context, index) {
          final todo = todos[index];
          return ListTile(
            title: Text(todo),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          _addTodo();
        },
        child: Icon(Icons.add),
      ),
    );
  }

  void _addTodo() async {
    final todo = await showDialog<String>(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Add Todo'),
          content: TextField(),
          actions: [
            FlatButton(
              child: Text('Cancel'),
              onPressed: () {
                Navigator.pop(context);
              },
            ),
            FlatButton(
              child: Text('Add'),
              onPressed: () {
                Navigator.pop(context, 'New Todo');
              },
            ),
          ],
        );
      },
    );

    if (todo != null) {
      setState(() {
        todos.add(todo);
      });
    }
  }
}
```

In the above code, we have defined a `TodoListPage` which is a StatefulWidget. Within its state, we have a list of todos which we will display using the ListView widget.

## Step 3: Run the app

Save the changes and run the app using the following command:

```bash
flutter run
```

You should now see the Todo List app running on your device or emulator. You can start adding todos by tapping on the floating action button.

## Conclusion

In this tutorial, we learned how to create a simple todo list app using ListView in Flutter. The ListView widget makes it easy to display a list of items on the screen and allows users to interact with them. Feel free to enhance the app by adding features like marking todos as completed or deleting them.

#Flutter #ListView