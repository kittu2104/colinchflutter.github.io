---
layout: post
title: "Card widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [design]
comments: true
share: true
---

In Flutter, there are two primary ways to create card-like UI elements: using the `Card` widget in `MaterialApp` or using the `CupertinoCard` widget in `CupertinoApp`. Both widgets have their own unique styles and design guidelines that align with the Material Design and Cupertino design principles, respectively. 

Let's dive into the similarities and differences between these two card widgets.

## Card Widget in MaterialApp

The `Card` widget is part of the Material Design library and is commonly used in `MaterialApp`-based applications. It provides a Material-themed card with rounded corners and elevation effects.

### Creating a Card

To create a `Card` widget, you can use the following code:

```dart
Card(
  child: ListTile(
    leading: Icon(Icons.album),
    title: Text('Card Title'),
    subtitle: Text('Card Subtitle'),
  ),
)
```

In this example, we have a `Card` widget that contains a `ListTile` with an icon, title, and subtitle. You can customize the appearance of the `Card` and its child widgets using properties such as `color`, `elevation`, `shape`, and more.

### Advantages of Card in MaterialApp

- Familiar Material Design style: The `Card` widget follows the Material Design guidelines, providing a consistent look and feel within your MaterialApp-based application.
- Well-integrated with other Material Design components: It seamlessly integrates with other Material Design components like `ListView`, `AppBar`, and `Container`, making it easy to build complex UI layouts.

## CupertinoCard Widget in CupertinoApp

The `CupertinoCard` widget is specific to Cupertino-style applications and follows the design guidelines of the iOS platform. It provides a card-like UI element with a unique visual style that aligns with Apple's design principles.

### Creating a CupertinoCard

To create a `CupertinoCard` widget, you can use the following code:

```dart
CupertinoCard(
  child: Column(
    children: [
      ListTile(
        leading: Icon(CupertinoIcons.circle),
        title: Text('Cupertino Card'),
        subtitle: Text('Cupertino Subtitle'),
      ),
      CupertinoButton(
        child: Text('Button'),
        onPressed: () {},
      ),
    ],
  ),
)
```

In this example, we have a `CupertinoCard` widget that contains a `ListTile` and a `CupertinoButton`. You can customize the appearance of the `CupertinoCard` and its child widgets using properties such as `color`, `elevation`, and `borderRadius`.

### Advantages of CupertinoCard in CupertinoApp

- Consistent with iOS design: The `CupertinoCard` widget follows the design principles of iOS, providing a familiar look and feel for CupertinoApp-based applications.
- Seamless integration with other Cupertino components: It works well with other Cupertino-style components like `CupertinoListTile`, `CupertinoButton`, and `CupertinoNavigationBar`, enabling you to create visually cohesive iOS experiences.

## Conclusion

Choosing between the `Card` widget in `MaterialApp` and the `CupertinoCard` widget in `CupertinoApp` depends on the platform-specific design guidelines you want to follow. If you are building an app that adheres to Material Design standards, the `Card` widget is the way to go. On the other hand, if you are targeting iOS users and want to provide a more native experience, the `CupertinoCard` widget is the better choice.

Remember, these are just the card widgets, and you can mix and match other widgets based on your design and functionality requirements in both `MaterialApp` and `CupertinoApp`.

#flutter #design