---
layout: post
title: "Customizing scroll physics for AnimatedSize and Flexible in Flutter"
description: " "
date: 2023-09-20
tags: [Flutter, ScrollPhysics]
comments: true
share: true
---

In Flutter, **AnimatedSize** and **Flexible** are commonly used widgets for building dynamic and animated user interfaces. However, when using these widgets in combination with scrollable widgets like **ListView** or **GridView**, you might notice that the animation or resizing behavior does not work as expected.

By default, widgets like AnimatedSize and Flexible use the **ScrollPhysics** of their parent scrollable widget. This can result in unexpected scroll behavior, especially when you want to have more control over the animation or resizing.

To overcome this limitation, you can customize the scroll physics to provide the desired behavior. Let's explore how you can achieve this.

## Customizing Scroll Physics for AnimatedSize

To create a custom scroll physics for AnimatedSize, you can use the **ClampingScrollPhysics** class, which provides the behavior of clamping the scroll offset. Here's an example of how you can use it:

```dart
AnimatedSize(
  vsync: this,
  duration: Duration(milliseconds: 500),
  curve: Curves.easeInOut,
  alignment: Alignment.center,
  child: ListView.builder(
    physics: ClampingScrollPhysics(),
    itemCount: 10,
    itemBuilder: (context, index) {
      return ListTile(
        title: Text('Item $index'),
      );
    },
  ),
)
```

In this example, we wrap the **ListView.builder** with AnimatedSize and set the physics property of the ListView to ClampingScrollPhysics. This ensures that the scroll behavior is clamped, allowing AnimatedSize to animate the widget size correctly.

## Customizing Scroll Physics for Flexible

If you want to customize the scroll physics for the Flexible widget, you can use the **BouncingScrollPhysics** class. BouncingScrollPhysics provides the behavior of bouncing when reaching the edge of a scrollable widget. Here's an example:

```dart
Flexible(
  child: ListView.builder(
    physics: BouncingScrollPhysics(),
    itemCount: 10,
    itemBuilder: (context, index) {
      return ListTile(
        title: Text('Item $index'),
      );
    },
  ),
)
```

In this example, we set the physics property of the ListView in the Flexible widget to BouncingScrollPhysics. This enables the bouncing effect when scrolling beyond the edges of the ListView.

## Conclusion

By customizing the scroll physics for AnimatedSize and Flexible widgets, you can achieve the desired animation and resizing behavior, even when combined with various scrollable widgets. The ClampingScrollPhysics and BouncingScrollPhysics classes provide different types of scroll behavior to suit your specific needs.

Remember to experiment with different scroll physics classes and adjust the animation and resizing parameters according to your UI requirements. Happy coding!

#Flutter #ScrollPhysics