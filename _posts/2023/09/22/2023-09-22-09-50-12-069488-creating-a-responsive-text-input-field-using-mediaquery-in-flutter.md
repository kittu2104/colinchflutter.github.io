---
layout: post
title: "Creating a responsive text input field using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: []
comments: true
share: true
---

In this tutorial, we'll learn how to create a responsive text input field in Flutter using the `MediaQuery` widget. This will allow our text input field to adjust its size based on the device's screen size.

## Prerequisites

Before we start, make sure you have Flutter installed on your machine and have a basic understanding of Flutter widgets.

## Step 1: Set up a new Flutter project

Create a new Flutter project using the following command:

```
flutter create responsive_text_input
```

## Step 2: Create the text input field widget

In the `lib` directory of your Flutter project, create a new file called `text_input_field.dart`, and add the following code:

```dart
import 'package:flutter/material.dart';

class ResponsiveTextInput extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.symmetric(horizontal: 16.0),
      child: TextFormField(
        decoration: InputDecoration(
          hintText: 'Enter text',
        ),
      ),
    );
  }
}
```

Here, we have created a `ResponsiveTextInput` widget that contains a `Container` with some padding, and a `TextFormField` widget inside it.

## Step 3: Make the text input field responsive

To make the text input field responsive, we'll use the `MediaQuery` widget. Modify the `ResponsiveTextInput` widget's build method as follows:

```dart
@override
Widget build(BuildContext context) {
  final screenWidth = MediaQuery.of(context).size.width;

  return Container(
    padding: EdgeInsets.symmetric(horizontal: screenWidth > 600 ? 32.0 : 16.0),
    child: TextFormField(
      decoration: InputDecoration(
        hintText: 'Enter text',
      ),
    ),
  );
}
```

In this updated code, we obtain the screen width using `MediaQuery.of(context).size.width`. We then conditionally set the padding of the container based on the screen width. If the screen width is greater than 600 pixels, we set a larger padding value of `32.0`, otherwise, we set a smaller padding value of `16.0`.

## Step 4: Use the responsive text input field in your app

Open the `lib/main.dart` file and replace the existing code with the following code:

```dart
import 'package:flutter/material.dart';
import 'text_input_field.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Text Input',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Responsive Text Input'),
        ),
        body: Center(
          child: Padding(
            padding: EdgeInsets.all(16.0),
            child: ResponsiveTextInput(),
          ),
        ),
      ),
    );
  }
}
```

We have added an import statement for the `text_input_field.dart` file and used the `ResponsiveTextInput` widget inside the `Center` widget's child.

## Conclusion

By using the `MediaQuery` widget, we have made our text input field responsive, adapting its size based on the screen width. This allows our Flutter app to provide a better user experience on different devices.