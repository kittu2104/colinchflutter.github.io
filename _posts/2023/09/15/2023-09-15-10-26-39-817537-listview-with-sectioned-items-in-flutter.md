---
layout: post
title: "ListView with sectioned items in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, listview, sectioneditems]
comments: true
share: true
---

In Flutter, the `ListView` widget is commonly used when displaying a list of items. While this widget works well for displaying a simple flat list, sometimes you may need to display items with sections. In this blog post, we will explore how to create a `ListView` with sectioned items in Flutter.

## Setting up the Project
Before we dive into the implementation, make sure you have Flutter and the Dart SDK installed on your machine. If you haven't created a Flutter project yet, run the following command:

```bash
flutter create sectioned_list_example
```

Once the project is created, navigate to the project directory:

```bash
cd sectioned_list_example
```

Next, open the project in your favorite code editor.

## Creating the SectionedListView Widget
To create a sectioned `ListView` widget, we'll use the `ListView.builder` constructor. 

First, define a list of data that represents the sections and their corresponding items. For example, let's create a list of Map objects, where each object represents a section and contains a key for the section title and a key for the list of items within that section.

```dart
List<Map<String, dynamic>> _data = [
  {
    'sectionTitle': 'Fruits',
    'items': ['Apple', 'Banana', 'Orange'],
  },
  {
    'sectionTitle': 'Vegetables',
    'items': ['Carrot', 'Broccoli', 'Tomato'],
  },
  {
    'sectionTitle': 'Dairy',
    'items': ['Milk', 'Cheese', 'Yogurt'],
  },
];
```

Next, define a function that returns the number of sections in the `_data` list. For this, we can simply return the length of the list.

```dart
int _sectionCount() {
  return _data.length;
}
```

Then, define a function that returns the total number of items within a section at a given `sectionIndex`. This can be done by accessing the 'items' key of the Map object at that index and returning the length of the items list.

```dart
int _itemCount(int sectionIndex) {
  return _data[sectionIndex]['items'].length;
}
```

Finally, implement the `SectionedListView` widget by using the `ListView.builder` constructor. In the `builder` property, we can define how each section and item should be rendered based on the section and item index.

```dart
ListView.builder(
  itemCount: _sectionCount(),
  itemBuilder: (BuildContext context, int sectionIndex) {
    String sectionTitle = _data[sectionIndex]['sectionTitle'];
    List<String> items = _data[sectionIndex]['items'];
    
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: <Widget>[
        Padding(
          padding: const EdgeInsets.all(8.0),
          child: Text(sectionTitle, style: TextStyle(fontSize: 18, fontWeight: FontWeight.bold)),
        ),
        ListView.builder(
          shrinkWrap: true,
          physics: NeverScrollableScrollPhysics(),
          itemCount: _itemCount(sectionIndex),
          itemBuilder: (BuildContext context, int itemIndex) {
            String item = items[itemIndex];
            
            return ListTile(
              title: Text(item),
            );
          },
        ),
      ],
    );
  },
)
```

In this case, we have nested a `ListView.builder` inside a `Column` to render both sections and items. The `shrinkWrap` property set to `true` and the `physics` property set to `NeverScrollableScrollPhysics()` ensure that the inner `ListView.builder` only takes up the necessary space and does not scroll.

Finally, you can use the `SectionedListView` widget wherever you need to display a sectioned list of items.

## Conclusion
By utilizing the `ListView.builder` constructor and a nested layout structure, we can easily create a sectioned `ListView` in Flutter. This allows us to organize and display items in a more structured manner. With this approach, you can now create more visually appealing and user-friendly lists in your Flutter applications.

#flutter #listview #sectioneditems