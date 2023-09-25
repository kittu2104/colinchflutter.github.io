---
layout: post
title: "How to use the FractionalTranslation widget with the Opacity widget"
description: " "
date: 2023-09-25
tags: [widgets]
comments: true
share: true
---

In Flutter, the `FractionalTranslation` widget allows you to transform the position of its child widget within its parent container. The `Opacity` widget, on the other hand, allows you to control the transparency of its child widget. Combining these two widgets can lead to interesting visual effects in your app.

Here's an example of how you can use the `FractionalTranslation` widget with the `Opacity` widget:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      width: 200,
      height: 200,
      color: Colors.blue,
      child: FractionalTranslation(
        translation: Offset(0.5, 0.5),
        child: Opacity(
          opacity: 0.5,
          child: Container(
            color: Colors.red,
          ),
        ),
      ),
    );
  }
}
```
In the above example, we have a blue container with a size of 200x200. Inside this container, we have a `FractionalTranslation` widget with `translation` set to `Offset(0.5, 0.5)`. This means that the child will be shifted by 50% of the container's width and height to the right and bottom, respectively.

Inside the `FractionalTranslation`, we have an `Opacity` widget with `opacity` set to `0.5`. This will make the child container semi-transparent. The child container itself has a red color.

By combining the `FractionalTranslation` and `Opacity` widgets, we can achieve a visually appealing effect where the red container is shifted and partially transparent within the blue container.

Remember to import the necessary Flutter packages at the top of your file:

```dart
import 'package:flutter/material.dart';
```

That's it! You can now use the `FractionalTranslation` widget with the `Opacity` widget to create unique visual effects in your Flutter app. 

#flutter #widgets