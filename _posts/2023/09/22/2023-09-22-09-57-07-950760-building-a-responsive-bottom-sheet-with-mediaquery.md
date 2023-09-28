---
layout: post
title: "Building a responsive bottom sheet with `MediaQuery`"
description: " "
date: 2023-09-22
tags: [responsivedesign]
comments: true
share: true
---

When it comes to building a responsive user interface, one of the key elements is the bottom sheet. A bottom sheet is a draggable panel that slides up from the bottom of the screen, commonly used for displaying additional information or actions.

In this post, we will explore how to build a responsive bottom sheet using the `MediaQuery` class in [Flutter](https://flutter.dev/) framework. Flutter is an open-source UI software development kit developed by Google.

### Getting Started

Before we start, make sure you have Flutter installed on your system. Once you have Flutter installed, create a new Flutter project using the following command:

```dart
flutter create bottom_sheet_example
```

Now, navigate to the newly created project directory:

```dart
cd bottom_sheet_example
```

### Implementation

1. Open `lib/main.dart` file in your preferred code editor.

2. Remove the default code and replace it with the following code:

   ```dart
   import 'package:flutter/material.dart';

   void main() {
     runApp(MyApp());
   }

   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return MaterialApp(
         debugShowCheckedModeBanner: false,
         home: Scaffold(
           appBar: AppBar(
             title: Text('Responsive Bottom Sheet'),
           ),
           body: MyHomePage(),
         ),
       );
     }
   }

   class MyHomePage extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Container(
         child: Center(
           child: ElevatedButton(
             onPressed: () {
               _showBottomSheet(context);
             },
             child: Text('Show Bottom Sheet'),
           ),
         ),
       );
     }

     void _showBottomSheet(BuildContext context) {
       showModalBottomSheet(
         context: context,
         builder: (BuildContext context) {
           return Container(
             height: MediaQuery.of(context).size.height * 0.4,
             child: Column(
               children: [
                 ListTile(
                   leading: Icon(Icons.info),
                   title: Text('Information'),
                 ),
                 ListTile(
                   leading: Icon(Icons.settings),
                   title: Text('Settings'),
                 ),
                 ListTile(
                   leading: Icon(Icons.help),
                   title: Text('Help'),
                 ),
               ],
             ),
           );
         },
       );
     }
   }
   ```

3. Save the file, and run the application using the following command:

   ```dart
   flutter run
   ```

   This will launch the application on the connected device or simulator/emulator.

4. You should see a simple app with a button labeled "Show Bottom Sheet" in the center of the screen.

5. Tap the button, and a bottom sheet will slide up from the bottom, displaying three `ListTile` widgets with icons and titles.

### Understanding the Code

In the code above, we define a simple Flutter application with a `MyApp` widget as the root widget. Inside the `MyApp` widget, we have a `Scaffold` with an `AppBar` and a `MyHomePage` widget as the body.

In the `MyHomePage` widget, we have a `Container` with a centered `ElevatedButton`. On button press, we call the `_showBottomSheet` method, which will display the bottom sheet using the `showModalBottomSheet` function.

The `showModalBottomSheet` function takes a `builder` parameter that returns the content of the bottom sheet. In the returned `Container`, we set the `height` property to 40% of the screen height using `MediaQuery.of(context).size.height`.

Inside the `Column`, we have three `ListTile` widgets, each having an `Icon` and a `Text` widget.

### Conclusion

Using the `MediaQuery` class, we can easily build responsive UI elements in Flutter. In this post, we covered how to create a responsive bottom sheet that adapts its size based on the screen height.

By understanding and leveraging the power of `MediaQuery`, you can create beautiful and responsive user interfaces in Flutter.

#flutter #responsivedesign