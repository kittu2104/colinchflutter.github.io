---
layout: post
title: "Creating a horizontal timeline UI using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [timeline]
comments: true
share: true
---

In this tutorial, we will learn how to create a horizontal timeline User Interface (UI) using the `ListView` widget in Flutter. 

## Setting up the Project

Before we dive into coding, make sure you have Flutter installed and a new Flutter project set up on your machine. You can follow the official [Flutter installation guide](https://flutter.dev/docs/get-started/install) to get started.

## Creating the Timeline UI

1. Create a new file called `timeline_screen.dart` and add the following code:

```dart
import 'package:flutter/material.dart';

class TimelineScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Timeline'),
      ),
      body: ListView.builder(
        scrollDirection: Axis.horizontal,
        itemCount: 10,
        itemBuilder: (BuildContext context, int index) {
          return Container(
            width: 150,
            margin: EdgeInsets.all(10),
            color: Colors.blue,
            child: Center(
              child: Text(
                'Event $index',
                style: TextStyle(
                  color: Colors.white,
                  fontSize: 18,
                ),
              ),
            ),
          );
        },
      ),
    );
  }
}
```

2. Open your main file (usually `main.dart`) and update the `void main()` function to navigate to the `TimelineScreen`:

```dart
import 'package:flutter/material.dart';
import 'timeline_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Timeline Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TimelineScreen(),
    );
  }
}
```

3. Run your Flutter app using the `flutter run` command. You should now see a horizontal timeline UI with 10 labeled events.

## Customizing the Timeline UI

To customize the timeline UI, you can modify the `Container` widget in the `ListView.builder`'s `itemBuilder`. You can change the width, colors, fonts, and other properties to match your desired design.

Feel free to experiment and add additional widgets or functionality to enhance the timeline UI according to your project's requirements.

## Conclusion

In this tutorial, we have learned how to create a horizontal timeline UI using the `ListView` widget in Flutter. We have also explored customizing the UI to match different design preferences. 

This can be a great starting point for building timelines in your Flutter applications. Happy coding!

#flutter #timeline