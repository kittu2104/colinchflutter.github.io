---
layout: post
title: "List view widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [userinterface]
comments: true
share: true
---

When developing a mobile application, you often need to display a list of items to users. Flutter provides two main options for implementing a list view: `ListView` in `MaterialApp` and `CupertinoApp`. In this blog post, we will explore the similarities and differences between these two widgets and discuss when to use each.

## MaterialApp

`MaterialApp` is the widget that implements Material Design, Google's design language for mobile and web applications. It provides a set of widgets that adhere to the Material Design guidelines. One of these widgets is `ListView`, which allows you to display a scrollable list of items vertically or horizontally.

Here's an example of using `ListView` in `MaterialApp`:

```
MaterialApp(
  home: Scaffold(
    appBar: AppBar(
      title: Text('ListView Example'),
    ),
    body: ListView(
      children: <Widget>[
        ListTile(
          leading: Icon(Icons.person),
          title: Text('John Doe'),
        ),
        ListTile(
          leading: Icon(Icons.person),
          title: Text('Jane Smith'),
        ),
        // more list tiles...
      ],
    ),
  ),
)
```

In this example, we create a simple list view with two list tiles containing icons and text. The `ListView` automatically scrolls when the content exceeds the available space.

`ListView` in `MaterialApp` provides additional features like dividers, headers, footers, and callbacks for item selection and scrolling. It also allows customization of the appearance through various properties and themes.

## CupertinoApp

`CupertinoApp` is the widget that implements the Cupertino design language, which is Apple's design language for iOS applications. It provides a set of widgets that offer the iOS look and feel.

Similar to `ListView` in `MaterialApp`, `CupertinoApp` also provides its own version of `ListView`, called `CupertinoListView`, which can be used to display a vertical or horizontal scrollable list of items.

Here's an example of using `CupertinoListView` in `CupertinoApp`:

```dart
CupertinoApp(
  home: CupertinoPageScaffold(
    navigationBar: CupertinoNavigationBar(
      middle: Text('ListView Example'),
    ),
    child: CupertinoListView(
      children: <Widget>[
        ListTile(
          leading: Icon(Icons.person),
          title: Text('John Doe'),
        ),
        ListTile(
          leading: Icon(Icons.person),
          title: Text('Jane Smith'),
        ),
        // more list tiles...
      ],
    ),
  ),
)
```

In this example, we create a similar list view as before, but this time, we use `CupertinoListView` inside `CupertinoApp`. The list view adopts the Cupertino look, with its own set of styling, animations, and behaviors specific to iOS.

`CupertinoListView` provides features like separators, section headers, and callbacks for item selection. It can also be customized using properties and themes specific to the Cupertino design language.

## When to Use Each

The choice between `ListView` in `MaterialApp` and `CupertinoListView` in `CupertinoApp` depends on the target platform and the design language you want to adhere to. If you are developing a cross-platform application and want to provide a consistent Material Design experience, you should use `ListView` inside `MaterialApp`. On the other hand, if your app is specifically for iOS and you want to follow the iOS design guidelines, you should opt for `CupertinoListView` inside `CupertinoApp`.

It's worth noting that Flutter provides widgets like `ListView.builder` and `ListView.separated` that can be used with either `MaterialApp` or `CupertinoApp` to create more dynamic and customizable list views.

In conclusion, both `MaterialApp` and `CupertinoApp` offer list view widgets that can be used to display scrollable lists of items. The choice between them ultimately depends on your target platform and the design language you want to follow.

#flutter #userinterface