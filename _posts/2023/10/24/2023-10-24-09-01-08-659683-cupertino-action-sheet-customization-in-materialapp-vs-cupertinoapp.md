---
layout: post
title: "Cupertino action sheet customization in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a mobile application, one key aspect is customizing the user interface to suit the platform's design aesthetics. In the case of iOS, Cupertino widgets provide a way to achieve a native look and feel. Two important widgets that allow customization of an action sheet are `MaterialApp` and `CupertinoApp`. In this blog post, we'll explore the customization options available for Cupertino action sheets in both `MaterialApp` and `CupertinoApp` and compare the differences between the two.

## Table of Contents
- [Introduction to Cupertino Action Sheets](#introduction-to-cupertino-action-sheets)
- [Customization in MaterialApp](#customization-in-materialapp)
- [Customization in CupertinoApp](#customization-in-cupertinoapp)
- [Differences Between MaterialApp and CupertinoApp](#differences-between-materialapp-and-cupertinoapp)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction to Cupertino Action Sheets
Cupertino action sheets are a form of modal dialog that display a set of options to the user. They are commonly used to present a menu of actions or prompt the user to make a choice. In iOS, action sheets are presented at the bottom of the screen and typically include a title, a set of buttons, and an optional cancel button.

## Customization in MaterialApp
When using `MaterialApp` as the base widget for your application, you can customize the appearance of the Cupertino action sheet to match the Material Design guidelines. You can modify the colors, fonts, and layout of the action sheet to align with the overall material theme of your app.

To customize the action sheet, you can use the `showModalBottomSheet` method provided by the `Scaffold` widget. This method allows you to pass a `builder` function that returns a widget tree representing the contents of the action sheet. Inside the builder function, you can use `Container`, `TextStyle`, and other widgets to customize the appearance.

```dart
showModalBottomSheet<void>(
  context: context,
  builder: (BuildContext context) {
    return Container(
      color: Colors.white,
      height: 200,
      child: Column(
        children: [
          Text(
            'Choose an option',
            style: TextStyle(
              fontSize: 18,
              fontWeight: FontWeight.bold,
            ),
          ),
          SizedBox(height: 16),
          ElevatedButton(
            onPressed: () {},
            child: Text('Option 1'),
          ),
          ElevatedButton(
            onPressed: () {},
            child: Text('Option 2'),
          ),
          TextButton(
            onPressed: () {},
            child: Text('Cancel'),
          ),
        ],
      ),
    );
  },
);
```

## Customization in CupertinoApp
If you want to achieve a more native and iOS-like appearance for your action sheet, you can use `CupertinoApp` as the base widget for your application. `CupertinoApp` provides a Cupertino-style action sheet that automatically adapts to the platform's styling.

To display a Cupertino action sheet, you can use `showCupertinoModalPopup` method provided by the `CupertinoButton` widget. Similar to `MaterialApp`, you can pass a `builder` function that returns the content of the action sheet. You can customize the appearance by using `CupertinoHeaderFooterBuilder`, `CupertinoActionSheetAction`, and other Cupertino-specific widgets.

```dart
showCupertinoModalPopup(
  context: context,
  builder: (BuildContext context) {
    return CupertinoActionSheet(
      title: Text('Choose an option'),
      actions: [
        CupertinoActionSheetAction(
          onPressed: () {},
          child: Text('Option 1'),
        ),
        CupertinoActionSheetAction(
          onPressed: () {},
          child: Text('Option 2'),
        ),
      ],
      cancelButton: CupertinoActionSheetAction(
        onPressed: () {},
        child: Text('Cancel'),
        isDefaultAction: true,
      ),
    );
  },
);
```

## Differences Between MaterialApp and CupertinoApp
While both `MaterialApp` and `CupertinoApp` provide ways to customize Cupertino action sheets, there are some key differences. 

1. **Visual Style:** `MaterialApp` allows you to customize the action sheet to match the material design guidelines, while `CupertinoApp` provides a more native iOS appearance out of the box.

2. **Widget Availability:** `MaterialApp` offers a wide range of Material Design widgets for customization, whereas `CupertinoApp` provides a specific set of Cupertino-specific widgets for achieving an iOS-like appearance.

3. **Platform Adaptation:** `MaterialApp` allows your app to easily run on both iOS and Android by adapting to platform-specific styling. On the other hand, `CupertinoApp` is primarily designed for iOS.

## Conclusion
Customizing the appearance of an action sheet is essential for creating a visually appealing and consistent user experience. Both `MaterialApp` and `CupertinoApp` offer ways to achieve this, with `MaterialApp` aligning with Material Design guidelines and `CupertinoApp` providing a native iOS-like appearance. By understanding their differences, developers can make informed decisions on which widget to use based on their target platform and desired visual style.

## References
- [Flutter Documentation - CupertinoActionSheet](https://api.flutter.dev/flutter/cupertino/CupertinoActionSheet-class.html)
- [Flutter Documentation - MaterialApp](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter Documentation - CupertinoApp](https://api.flutter.dev/flutter/cupertino/CupertinoApp-class.html)