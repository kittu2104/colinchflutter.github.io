---
layout: post
title: "ListView with divided sections in Flutter."
description: " "
date: 2023-09-15
tags: [ListView, MobileDevelopment]
comments: true
share: true
---

One common UI pattern in mobile app development is to display a list of items divided into multiple sections. In Flutter, we can achieve this using the `ListView` widget along with the `ListTile` widget for individual items.

## Setting up the ListView

To begin, add a `ListView.builder` widget to your Flutter app's UI. This widget allows us to build the list dynamically based on the provided data.

```dart
ListView.builder(
  itemCount: sectionData.length,
  itemBuilder: (BuildContext context, int index) {
    return Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: <Widget>[
        SectionHeader(title: sectionData[index].title),
        ListView.builder(
          shrinkWrap: true,
          physics: NeverScrollableScrollPhysics(),
          itemCount: sectionData[index].items.length,
          itemBuilder: (BuildContext context, int itemIndex) {
            return ListTile(
              title: Text(sectionData[index].items[itemIndex]),
            );
          },
        ),
      ],
    );
  },
)
```
## Defining the SectionHeader widget

In the code above, we have used a custom widget called `SectionHeader` to display the section title. Here's an example implementation:

```dart
class SectionHeader extends StatelessWidget {
  final String title;

  SectionHeader({required this.title});

  @override
  Widget build(BuildContext context) {
    return Container(
      padding: EdgeInsets.symmetric(horizontal: 16, vertical: 8),
      child: Text(title,
          style: TextStyle(
            fontWeight: FontWeight.bold,
            fontSize: 16,
          )),
    );
  }
}
```

## Data structure for sections and items

To display the divided sections, you need to have a data structure to hold the section titles and their respective items. For example, you can create a class called `SectionData` as shown below:

```dart
class SectionData {
  final String title;
  final List<String> items;

  SectionData({required this.title, required this.items});
}

List<SectionData> sectionData = [
  SectionData(
    title: 'Section 1',
    items: ['Item 1', 'Item 2', 'Item 3'],
  ),
  SectionData(
    title: 'Section 2',
    items: ['Item 4', 'Item 5'],
  ),
];
```

## Conclusion

By utilizing the `ListView` and `ListTile` widgets in Flutter, you can easily create a list with divided sections. The provided code snippet shows how to dynamically build the sections and display them using the `SectionHeader` widget. Remember to customize the styling and data structure to fit your specific needs!

#flutter #ListView #UI #MobileDevelopment