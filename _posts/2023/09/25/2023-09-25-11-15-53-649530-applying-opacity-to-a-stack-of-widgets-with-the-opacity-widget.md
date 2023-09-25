---
layout: post
title: "Applying opacity to a stack of widgets with the Opacity widget"
description: " "
date: 2023-09-25
tags: []
comments: true
share: true
---

To use the Opacity widget, follow these steps:

First, wrap the stack of widgets that you want to apply opacity to with the Opacity widget. The Opacity widget takes two parameters: `opacity` and `child`.

The `opacity` parameter accepts a value between 0.0 and 1.0, where 0.0 represents completely transparent and 1.0 represents fully opaque. You can adjust the opacity level depending on your requirements.

Here's an example of applying a 50% opacity to a stack of widgets:

```dart
Opacity(
  opacity: 0.5,
  child: Stack(
    children: [
      // Add your widgets here...
    ],
  ),
)
```

In this example, the stack of widgets will be rendered with 50% opacity. You can adjust the `opacity` parameter to any value between 0.0 and 1.0 to achieve the desired transparency level.

Remember to replace `// Add your widgets here...` with the actual widgets you want to display within the stack.

Using the Opacity widget allows you to create visually appealing UIs by applying varying levels of transparency to stacked widgets.