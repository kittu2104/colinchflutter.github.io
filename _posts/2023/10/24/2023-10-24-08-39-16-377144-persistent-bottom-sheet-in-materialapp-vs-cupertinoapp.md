---
layout: post
title: "Persistent bottom sheet in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [MobileDevelopment]
comments: true
share: true
---

When developing a mobile application, having a persistent bottom sheet is a common requirement. It's a powerful way to display additional information or options while still keeping the main content visible. In Flutter, you can achieve this using either the `MaterialApp` or `CupertinoApp` widgets, depending on the platform-specific design you want to follow.

### MaterialApp Bottom Sheet

The `MaterialApp` widget is for building apps that follow Material Design guidelines, which is the default design language for Android. To create a persistent bottom sheet in a `MaterialApp`, you can use the `showBottomSheet` method provided by `ScaffoldState`, which is accessible from the `BuildContext`. 

Here's an example of how you can create a persistent bottom sheet in a `MaterialApp`:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('My App'),
        ),
        body: Center(
          child: RaisedButton(
            child: Text('Show Bottom Sheet'),
            onPressed: () {
              showModalBottomSheet(
                context: context,
                builder: (context) {
                  return Container(
                    height: 200,
                    child: Center(
                      child: Text('This is a persistent bottom sheet.'),
                    ),
                  );
                },
              );
            },
          ),
        ),
      ),
    );
  }
}

```

In this example, when the "Show Bottom Sheet" button is pressed, the `showModalBottomSheet` method is called. Inside the `builder` parameter, you can customize the content of the bottom sheet. In this case, we are simply displaying a centered text message.

### CupertinoApp Bottom Sheet

If you want your app to adhere to iOS design guidelines, you can use the `CupertinoApp` widget. To create a persistent bottom sheet in a `CupertinoApp`, you can use the `showCupertinoModalPopup` method provided by `BuildContext`.

Here's an example of how you can create a persistent bottom sheet in a `CupertinoApp`:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('My App'),
        ),
        child: Center(
          child: CupertinoButton(
            child: Text('Show Bottom Sheet'),
            onPressed: () {
              showCupertinoModalPopup(
                context: context,
                builder: (context) {
                  return Container(
                    height: 200,
                    child: Center(
                      child: Text('This is a persistent bottom sheet.'),
                    ),
                  );
                },
              );
            },
          ),
        ),
      ),
    );
  }
}
```

Similar to the `MaterialApp` example, we are using the `showCupertinoModalPopup` method to display the bottom sheet. In this case, the method is called when the button is pressed, and the content of the sheet is a centered text message.

### Conclusion

Whether you are developing for Android or iOS, Flutter provides you with the flexibility to create persistent bottom sheets that match the design language of each platform. By using `showModalBottomSheet` in a `MaterialApp` or `showCupertinoModalPopup` in a `CupertinoApp`, you can easily implement this feature in your Flutter application.

---

**References:**

- Flutter Documentation: [BottomSheet](https://api.flutter.dev/flutter/material/showModalBottomSheet.html)
- Flutter Documentation: [CupertinoPopover](https://api.flutter.dev/flutter/cupertino/showCupertinoModalPopup.html)

**#Flutter** **#MobileDevelopment**