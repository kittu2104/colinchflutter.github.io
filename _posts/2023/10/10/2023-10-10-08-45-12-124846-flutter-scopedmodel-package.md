---
layout: post
title: "Flutter ScopedModel package"
description: " "
date: 2023-10-10
tags: [scopedmodel]
comments: true
share: true
---

When it comes to managing the state in a Flutter application, things can quickly become complex and challenging. Flutter provides various options for state management, and one popular package that simplifies this process is ScopedModel.

ScopedModel is a Flutter package that provides a simple yet powerful way to manage state in your application. It utilizes the InheritedWidget feature of Flutter to propagate changes to the required widgets efficiently.

In this blog post, we will explore the ScopedModel package and learn how it can help simplify state management in your Flutter apps.

## What is ScopedModel?

ScopedModel is a lightweight state management solution for Flutter applications. It follows the Scoped Model design pattern, which allows you to define and manage the application state in a hierarchical structure.

The package consists of three main components:
1. **Model**: A class that holds the application state and notifies the listeners when the state changes.
2. **ScopedModel**: An InheritedWidget that propagates the model to the descendant widgets.
3. **ScopedModelDescendant**: A widget that listens to changes in the model and rebuilds itself when necessary.

## Installation

To use the ScopedModel package in your Flutter project, add the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  scoped_model: ^1.1.0
```

Then, run `flutter pub get` to fetch the package.

## Getting Started with ScopedModel

To start using ScopedModel, you need to follow a few simple steps:

1. Create a model class that extends the `Model` class provided by the ScopedModel package.
2. Add the state variables and methods to your model class.
3. Wrap your widget tree with a `ScopedModel` widget and provide an instance of your model class.
4. Use the `ScopedModelDescendant` widget to access and update the state from various parts of your widget tree.

Here's an example of how you can use ScopedModel to manage a counter state in a Flutter application:

```dart
import 'package:flutter/material.dart';
import 'package:scoped_model/scoped_model.dart';

// Step 1: Create a model class that extends Model
class CounterModel extends Model {
  int _count = 0;

  // Step 2: Add state variables and methods
  int get count => _count;

  void increment() {
    _count++;
    notifyListeners(); // Notify the listeners about the state change
  }
}

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  // Step 3: Wrap your widget tree with ScopedModel
  @override
  Widget build(BuildContext context) {
    return ScopedModel<CounterModel>(
      model: CounterModel(),
      child: MaterialApp(
        home: HomePage(),
      ),
    );
  }
}

class HomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ScopedModelDescendant<CounterModel>(
      builder: (context, child, model) {
        // Step 4: Use ScopedModelDescendant to access and update the state
        return Scaffold(
          appBar: AppBar(
            title: Text('ScopedModel Counter'),
          ),
          body: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Text(
                  'Count',
                  style: TextStyle(fontSize: 24),
                ),
                Text(
                  '${model.count}', // Access the state from the model
                  style: TextStyle(fontSize: 48, fontWeight: FontWeight.bold),
                ),
              ],
            ),
          ),
          floatingActionButton: FloatingActionButton(
            onPressed: model.increment, // Update the state using model methods
            child: Icon(Icons.add),
          ),
        );
      },
    );
  }
}
```

In this example, we create a `CounterModel` class that extends `Model` and holds a `count` variable. We use the `ScopedModel` widget to provide an instance of this model to the widget tree, and then we use the `ScopedModelDescendant` widget to access and update the state from the `HomePage` widget.

Whenever the `increment` method is called, the `_count` variable is updated, and the `ScopedModelDescendant` widget rebuilds itself, reflecting the updated state.

## Conclusion

ScopedModel is a powerful package for state management in Flutter applications. It simplifies the management and propagation of application state using the Scoped Model design pattern. By using ScopedModel, you can effectively manage your state and make your Flutter apps more scalable and maintainable.

Give ScopedModel a try in your next Flutter project and experience the benefits of simplified state management.

#flutter #scopedmodel