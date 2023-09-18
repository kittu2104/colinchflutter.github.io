---
layout: post
title: "Implementing a timeline view with ListView in Flutter."
description: " "
date: 2023-09-15
tags: [TimelineView]
comments: true
share: true
---

As mobile app developers, we often come across the need to display data in a timeline format. One way to achieve this in Flutter is by using the `ListView` widget along with some custom styling. In this blog post, we will explore how to implement a timeline view using `ListView` in Flutter.

## Setting up the project

Before we begin, make sure you have Flutter installed on your machine. You can do this by following the official Flutter installation guide.

Create a new Flutter project by running the following command in your terminal:

```bash
$ flutter create timeline_view_flutter
```

Change to the project directory:

```bash
$ cd timeline_view_flutter
```

Open the project in your preferred code editor.

## Adding dependencies

To create the timeline view, we will be using the `flutter_timeline` package. Add the following line to the `dependencies` section in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_timeline: ^1.0.0
```

Save the changes and run `flutter pub get` to fetch the package.

## Implementing the timeline view

Now, let's create a new file called `timeline_view.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_timeline/flutter_timeline.dart';

class TimelineView extends StatelessWidget {
  final List<String> events = ['Event 1', 'Event 2', 'Event 3'];
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Timeline View'),
      ),
      body: ListView.builder(
        itemCount: events.length,
        itemBuilder: (context, index) {
          return TimelineTile(
            alignment: TimelineAlign.manual,
            lineXY: 0.2,
            isFirst: index == 0,
            isLast: index == events.length - 1,
            beforeLineStyle: LineStyle(color: Colors.grey),
            afterLineStyle: LineStyle(color: Colors.grey),
            indicatorStyle: IndicatorStyle(
              width: 40,
              height: 40,
              indicator: Container(
                decoration: BoxDecoration(
                  color: Colors.blue,
                  shape: BoxShape.circle,
                ),
                child: Center(
                  child: Text(
                    '${index + 1}',
                    style: TextStyle(color: Colors.white),
                  ),
                ),
              ),
            ),
            startChild: Text(events[index]),
          );
        },
      ),
    );
  }
}
```

In the above code, we have created a `TimelineView` class that extends `StatelessWidget`. We have defined a list of `events` which will be displayed in the timeline view. Inside the `build` method, we have used `ListView.builder` to iterate over the `events` list and create a `TimelineTile` for each event. 

We have also set various properties of the `TimelineTile` to customize its appearance, such as the alignment, line style, indicator style, and the child widget to display for each event.

## Running the app

To test the timeline view, open your main.dart file and replace its contents with the following code:

```dart
	import 'package:flutter/material.dart';
	import 'timeline_view.dart';
	
	void main() {
	  runApp(MyApp());
	}
	
	class MyApp extends StatelessWidget {
	  @override
	  Widget build(BuildContext context) {
	    return MaterialApp(
	      title: 'Timeline View',
	      theme: ThemeData(
	        primarySwatch: Colors.blue,
	      ),
	      home: TimelineView(),
	    );
	  }
	}
```

Save the changes and run the app using the following command:

```bash
$ flutter run
```

You should see a timeline view with the events displayed on your emulator or device.

## Conclusion

In this blog post, we have learned how to implement a timeline view using `ListView` in Flutter. By using the `flutter_timeline` package, we were able to create a timeline view with custom styling. You can further customize the appearance of the timeline by modifying the properties of `TimelineTile` and `IndicatorStyle`. We hope this tutorial has been helpful in achieving your desired timeline view in your Flutter project.

## #Flutter #TimelineView