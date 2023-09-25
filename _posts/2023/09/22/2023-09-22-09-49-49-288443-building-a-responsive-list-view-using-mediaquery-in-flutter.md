---
layout: post
title: "Building a responsive list view using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [responsive]
comments: true
share: true
---

In this tutorial, we will explore how to build a responsive list view in Flutter using the `MediaQuery` class. `MediaQuery` provides information about the current media environment, such as screen size and orientation, which allows us to create a responsive UI that adapts to different screen sizes and devices.

## Step 1: Set up the project

First, let's create a new Flutter project by running the following command in your terminal:

```dart
flutter create responsive_list_view
cd responsive_list_view
```

## Step 2: Create the list view widget

Inside the `lib` folder, create a new file called `list_view.dart`. In this file, we will define our list view widget.

```dart
import 'package:flutter/material.dart';

class ListViewWidget extends StatelessWidget {
  const ListViewWidget({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: 10,
      itemBuilder: (BuildContext context, int index) {
        return ListTile(
          title: Text('Item $index'),
        );
      },
    );
  }
}
```

## Step 3: Build the responsive layout

Inside the `lib` folder, open the `main.dart` file. Replace the default content with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:responsive_list_view/list_view.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive List View',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive List View'),
        ),
        body: SafeArea(
          child: MediaQuery.of(context).size.width > 600 ? Center(child: Text('Tablet Layout')) : ListViewWidget(),
        ),
      ),
    );
  }
}
```

In the above code, we use the `MediaQuery` class to check the width of the current device's screen. If the width is greater than 600 (considered as a tablet layout), we display a centered text 'Tablet Layout'. Otherwise, we display the `ListViewWidget` we defined earlier.

## Step 4: Run the app

Save the file and run the app using the following command:

```dart
flutter run
```

You should now see the app running with a responsive list view that adapts to different screen sizes. Play around with different screen sizes, orientations, and devices to see the responsive behavior in action.

#flutter #responsive #listview