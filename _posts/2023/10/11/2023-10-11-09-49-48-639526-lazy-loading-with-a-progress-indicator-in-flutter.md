---
layout: post
title: "Lazy loading with a progress indicator in Flutter"
description: " "
date: 2023-10-11
tags: []
comments: true
share: true
---

One common challenge in mobile app development is handling the loading and display of large amounts of data. When dealing with data-heavy applications, it's crucial to implement lazy loading to improve performance and user experience. 

Lazy loading is the technique of loading data only when it's needed, rather than loading all data upfront. In Flutter, lazy loading can be achieved using the `ListView.builder` widget, which creates a scrollable list of items on demand. 

## Setting up the Project

Before we dive into lazy loading, let's set up a basic Flutter project. Assuming you have Flutter installed, open your terminal and run the following commands:

```bash
flutter create lazy_loading_demo
cd lazy_loading_demo
```

Open the project in your favorite code editor and navigate to the `lib/main.dart` file. Replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Lazy Loading Demo'),
        ),
        body: MyListView(),
      ),
    );
  }
}

class MyListView extends StatefulWidget {
  @override
  _MyListViewState createState() => _MyListViewState();
}

class _MyListViewState extends State<MyListView> {
  List<int> items = [];

  @override
  void initState() {
    super.initState();
    fetchData();
  }

  Future<void> fetchData() async {
    // Simulating an API call with a delay of 2 seconds
    await Future.delayed(Duration(seconds: 2));

    // Generating a list of items
    List<int> newItems = List.generate(20, (index) => index + items.length);
  
    setState(() {
      items.addAll(newItems);
    });
  }

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: items.length + 1,
      itemBuilder: (BuildContext context, int index) {
        if (index == items.length) {
          return _buildProgressIndicator();
        } else {
          return ListTile(
            title: Text('Item ${items[index]}'),
          );
        }
      },
    );
  }

  Widget _buildProgressIndicator() {
    return Padding(
      padding: EdgeInsets.all(16.0),
      child: Center(
        child: CircularProgressIndicator(),
      ),
    );
  }
}
```

In the code above, we create a basic Flutter application with a `ListView.builder` widget inside the `MyListView` widget. The `items` list initially starts empty and will be populated with 20 items after a 2-second delay to simulate an API call.

The `ListView.builder` checks if the current item index is equal to the length of the `items` list. If it is, it returns a progress indicator widget `_buildProgressIndicator()`, otherwise it renders a `ListTile` widget with the corresponding item text.

The `_buildProgressIndicator` method returns a circular progress indicator centered on the screen as feedback while new data is being loaded.

## Running the App

To run the Flutter application, execute the following command in your terminal:

```bash
flutter run
```

Make sure you have an active simulator running or a physical device connected to your development machine.

## Conclusion

Implementing lazy loading with a progress indicator is an effective way to handle large datasets in your Flutter applications. By loading data only when it's needed, you can significantly improve performance and provide a better user experience. With the powerful `ListView.builder` widget, it's easy to achieve lazy loading and display a progress indicator while new items are being loaded.