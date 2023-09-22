---
layout: post
title: "Creating a responsive tab view using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, responsivedesign]
comments: true
share: true
---

In Flutter, building a responsive UI is essential for providing a seamless user experience across different devices and screen sizes. One common UI pattern is a tab view, where the content changes based on the selected tab. In this tutorial, we will learn how to create a responsive tab view using `MediaQuery` in Flutter.

## Step 1: Create a TabController

First, we need to create a `TabController` to manage the state of the tabs. We will define the number of tabs and their content in this step. Let's declare a `TabController` with three tabs:

```dart
TabController _tabController;

@override
void initState() {
  super.initState();
  _tabController = TabController(length: 3, vsync: this);
}
```

## Step 2: Create TabBar and TabBarView

Next, we need to create a `TabBar` to display the tabs and a `TabBarView` to display the corresponding content. We will use the `MediaQuery` to determine the screen size and adjust the layout accordingly.

```dart
@override
Widget build(BuildContext context) {
  final double screenWidth = MediaQuery.of(context).size.width;

  return Scaffold(
    appBar: AppBar(
      title: Text('Responsive Tab View'),
      bottom: TabBar(
        controller: _tabController,
        tabs: [
          Tab(text: 'Tab 1'),
          Tab(text: 'Tab 2'),
          Tab(text: 'Tab 3'),
        ],
      ),
    ),
    body: TabBarView(
      controller: _tabController,
      children: [
        if (screenWidth >= 600)
          _buildContent('Content for Tab 1'),
        if (screenWidth >= 600)
          _buildContent('Content for Tab 2'),
        _buildContent('Content for Tab 3'),
      ],
    ),
  );
}

Widget _buildContent(String text) {
  return Center(
    child: Text(text),
  );
}
```

In the above code, we conditionally render the content based on the screen width using the `if` statement. If the screen width is greater than or equal to 600, we show the content for Tab 1 and Tab 2. Otherwise, we only display the content for Tab 3.

## Step 3: Clean up resources

Don't forget to dispose of the `TabController` in the `dispose` method to release any resources it holds.

```dart
@override
void dispose() {
  _tabController.dispose();
  super.dispose();
}
```

That's it! Now you have a responsive tab view that adjusts its layout based on the screen size in Flutter. You can further customize the appearance and behavior of the tabs and content to match your app's design.

#flutter #responsivedesign