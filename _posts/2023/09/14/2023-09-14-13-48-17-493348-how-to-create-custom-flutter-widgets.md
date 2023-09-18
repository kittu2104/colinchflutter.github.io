---
layout: post
title: "How to create custom Flutter widgets"
description: " "
date: 2023-09-14
tags: [customwidgets]
comments: true
share: true
---

In Flutter, widgets are the building blocks of user interfaces. By default, Flutter offers a wide range of widgets that you can use to create your app's UI. However, there might be cases where you need to create your own custom widgets to meet specific design requirements or functionality. In this tutorial, we'll explore the process of creating custom Flutter widgets.

## Step 1: Define the Widget Class

To create a custom widget, you need to define a new class that extends either `StatelessWidget` if your widget is stateless, or `StatefulWidget` if your widget needs to maintain state. Let's start by creating a stateless widget called `CustomButton`:

```dart
class CustomButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      height: 50,
      width: 120,
      decoration: BoxDecoration(
        color: Colors.blue,
        borderRadius: BorderRadius.circular(8),
      ),
      child: Center(
        child: Text(
          'Custom Button',
          style: TextStyle(
            color: Colors.white,
            fontSize: 16,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
```

Here, we have defined a `CustomButton` widget that renders a blue rectangular button with custom text style.

## Step 2: Use the Custom Widget

Once you have defined your custom widget, you can use it just like any other built-in Flutter widget. Add an instance of `CustomButton` to your app's UI hierarchy using the `CustomButton()` constructor:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom Widget Example'),
        ),
        body: Center(
          child: CustomButton(),
        ),
      ),
    );
  }
}
```

Now, when you run your app, you should see the custom button widget rendered on the screen.

## Step 3: Adding Custom Properties

To make your custom widget more versatile, you can add custom properties that can be configured when using the widget. For example, let's say we want to allow the text and background color of our custom button to be customizable. To do this, we can add properties to the `CustomButton` class:

```dart
class CustomButton extends StatelessWidget {
  final String text;
  final Color backgroundColor;

  CustomButton({this.text, this.backgroundColor});

  @override
  Widget build(BuildContext context) {
    return Container(
      height: 50,
      width: 120,
      decoration: BoxDecoration(
        color: backgroundColor,
        borderRadius: BorderRadius.circular(8),
      ),
      child: Center(
        child: Text(
          text,
          style: TextStyle(
            color: Colors.white,
            fontSize: 16,
            fontWeight: FontWeight.bold,
          ),
        ),
      ),
    );
  }
}
```

Now, you can pass the text and background color when using the `CustomButton` widget:

```dart
CustomButton(
  text: 'Custom Button',
  backgroundColor: Colors.blue,
)
```

## Conclusion

Creating custom widgets in Flutter allows you to create reusable UI components that fit your app's specific requirements. By following the steps outlined in this tutorial, you should now have a good understanding of how to create and use custom widgets in Flutter. Experiment with different design patterns and functionalities to enhance your app's user interface and user experience.

#flutter #customwidgets