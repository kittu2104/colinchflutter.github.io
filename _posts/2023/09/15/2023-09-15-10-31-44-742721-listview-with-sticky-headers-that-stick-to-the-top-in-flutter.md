---
layout: post
title: "ListView with sticky headers that stick to the top in Flutter."
description: " "
date: 2023-09-15
tags: [StickyHeaders]
comments: true
share: true
---

When building a Flutter app, you might come across a requirement to display a list of items with sticky headers that stick to the top as you scroll. This is a common pattern seen in many apps, such as contacts or social media feeds. In this blog post, we will explore how to achieve this behavior using the `ListView` widget in Flutter.

## Setting up the ListView

To start, we need to set up a `ListView.builder` widget. This widget allows us to build a scrollable list of items efficiently by lazily creating the items as they become visible. Here's an example of how you can set up a basic `ListView.builder`:

```dart
ListView.builder(
  itemCount: _data.length,
  itemBuilder: (context, index) {
    // Build each item in the list
    return ListTile(
      title: Text(_data[index].title),
      subtitle: Text(_data[index].subtitle),
    );
  },
)
```

## Adding sticky headers

To make the headers sticky, we need to introduce a new widget called `SliverList`. This widget allows us to build a list with custom headers and sticky behavior. We can wrap our `ListView.builder` inside a `CustomScrollView` widget and use the `slivers` property to define our sticky headers and list items.

Here's an updated example that demonstrates how to add sticky headers:

```dart
CustomScrollView(
  slivers: [
    SliverList(
      delegate: SliverChildBuilderDelegate(
        (context, index) {
          // Build the header
          if (index.isEven) {
            return Container(
              height: 50,
              color: Colors.grey,
              child: Center(
                child: Text(
                  'Header ${index ~/ 2}',
                  style: TextStyle(
                    fontWeight: FontWeight.bold,
                  ),
                ),
              ),
            );
          }
          // Build each item in the list
          return ListTile(
            title: Text(_data[index ~/ 2].title),
            subtitle: Text(_data[index ~/ 2].subtitle),
          );
        },
        childCount: _data.length * 2,
      ),
    ),
  ],
)
```

In this example, we use the `SliverChildBuilderDelegate` to build both the headers and list items. We check if the index is even to determine if it's a header or a list item. The header container is given a fixed height and a grey background color, and the text is styled with a bold font weight.

## Conclusion

With the help of `CustomScrollView` and `SliverList`, we can easily create a ListView with sticky headers that stick to the top as you scroll. This pattern is useful when designing apps that display categorized content, such as contacts or social media feeds.

By implementing this behavior, you can provide a smooth and intuitive user experience in your Flutter app. Happy coding!

#Flutter #StickyHeaders