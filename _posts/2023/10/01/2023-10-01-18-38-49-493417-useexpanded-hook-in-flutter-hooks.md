---
layout: post
title: "useExpanded hook in Flutter Hooks"
description: " "
date: 2023-10-01
tags: [flutterhooks]
comments: true
share: true
---

Flutter Hooks is a powerful library that enhances the functionality of Flutter widgets by providing hooks for managing state and performing side-effects. One of the hooks provided by Flutter Hooks is the `useExpanded` hook, which can be used to control the expansion of a widget.

The `useExpanded` hook allows you to conditionally expand or collapse a widget based on a boolean state value. Let's see how we can use the `useExpanded` hook in a Flutter application.

First, make sure you have installed the Flutter Hooks package by adding it to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_hooks: ^0.18.0
```

Next, import the required packages in your Dart file:

```dart
import 'package:flutter_hooks/flutter_hooks.dart';
```

Now, let's create a widget that can be expanded or collapsed using the `useExpanded` hook:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_hooks/flutter_hooks.dart';

class ExpandableWidget extends HookWidget {
  @override
  Widget build(BuildContext context) {
    final expanded = useState(false);
    
    return Container(
      color: Colors.grey,
      child: Column(
        children: [
          ListTile(
            title: Text('Expandable Widget'),
            trailing: IconButton(
              icon: Icon(expanded.value? Icons.expand_less : Icons.expand_more),
              onPressed: () {
                expanded.value = !expanded.value;
              },
            ),
          ),
          if (expanded.value) // Conditional rendering using expanded.value
            Padding(
              padding: EdgeInsets.all(16.0),
              child: Text('This is the expanded content'),
            ),
        ],
      ),
    );
  }
}
```

In the above example, we create a `useState` hook to manage the boolean state named `expanded`. We then use this state value to conditionally render the expanded content in the `if` statement.

Finally, you can use the `ExpandableWidget` in your Flutter app like any other widget:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Flutter Hooks Example'),
        ),
        body: Center(
          child: ExpandableWidget(),
        ),
      ),
    );
  }
}
```

By using the `useExpanded` hook, you can easily add expandable behavior to any widget in your Flutter application. It provides a clean and concise way to manage the expansion state of a widget.

#flutter #flutterhooks