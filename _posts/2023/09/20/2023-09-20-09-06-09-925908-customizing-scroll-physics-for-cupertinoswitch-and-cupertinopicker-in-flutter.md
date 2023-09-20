---
layout: post
title: "Customizing scroll physics for CupertinoSwitch and CupertinoPicker in Flutter"
description: " "
date: 2023-09-20
tags: [iOSWidgets]
comments: true
share: true
---

When working with **Flutter**, you may come across scenarios where you need to customize the scroll physics for the `CupertinoSwitch` or `CupertinoPicker` widgets. These widgets provide a native iOS look and feel to your app, but by default, they use standard scroll physics. In certain cases, you might want to adjust the scrolling behavior to better suit your app's requirements. In this article, we'll explore how you can achieve this customization.


## CupertinoSwitch

The `CupertinoSwitch` widget is used to represent a toggle switch in iOS-style. By default, it uses the `BouncingScrollPhysics` for scroll physics. However, you can easily customize the scroll physics by providing your own `ScrollPhysics` object.


To customize the scroll physics for `CupertinoSwitch`, you can wrap it inside a `ScrollConfiguration` widget and override the `CupertinoScrollBehavior`. Here's an example:

```dart
ScrollConfiguration(
  behavior: CupertinoScrollBehavior(),
  child: CupertinoSwitch(
    value: true,
    onChanged: (value) { /* Your code here */ },
  ),
)
```

In the above example, we wrap the `CupertinoSwitch` widget with a `ScrollConfiguration` widget. We then set the `behavior` property to `CupertinoScrollBehavior()`. By doing this, we apply the custom scroll physics to the `CupertinoSwitch` widget. You can further customize the `CupertinoScrollBehavior` if needed, by providing additional parameters.


## CupertinoPicker

The `CupertinoPicker` widget is used to display a scrollable wheel with a set of options. Similar to `CupertinoSwitch`, it also uses the `BouncingScrollPhysics` by default. To customize the scroll physics for `CupertinoPicker`, we can follow a similar approach as with `CupertinoSwitch`.


Wrap the `CupertinoPicker` widget inside a `ScrollConfiguration` widget and provide your own `ScrollPhysics` object. Here's an example:

```dart
ScrollConfiguration(
  behavior: CupertinoScrollBehavior(),
  child: CupertinoPicker(
    itemExtent: 48, // Set the height of each item
    onSelectedItemChanged: (index) { /* Your code here */ },
    children: [
      Text('Option 1'),
      Text('Option 2'),
      Text('Option 3'),
    ],
  ),
)
```

In the above example, we wrap the `CupertinoPicker` widget with a `ScrollConfiguration` widget, which applies our custom scroll physics. We set the `behavior` property to `CupertinoScrollBehavior()`. You can tweak the `CupertinoScrollBehavior` according to your requirements.


## Conclusion

Customizing scroll physics for `CupertinoSwitch` and `CupertinoPicker` in Flutter is straightforward. By wrapping the widget in a `ScrollConfiguration` widget and providing your own `ScrollPhysics` object, you can easily adjust the scrolling behavior to suit your needs. This allows you to create a more tailored user experience for your iOS-style widgets.


#Flutter #iOSWidgets