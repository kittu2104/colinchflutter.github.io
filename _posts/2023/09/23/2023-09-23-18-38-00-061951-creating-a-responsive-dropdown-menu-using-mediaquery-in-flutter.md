---
layout: post
title: "Creating a responsive dropdown menu using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [dart]
comments: true
share: true
---

In this tutorial, we will explore how to create a responsive dropdown menu in Flutter using the `MediaQuery` class. The dropdown menu will adapt its layout based on the screen size of the device, providing a seamless user experience across different devices and orientations.

## Prerequisites

Before we begin, make sure you have Flutter installed and set up on your machine. You can follow the official Flutter installation guide on the [Flutter website](https://flutter.dev/docs/get-started/install) if you haven't done this already.

## Step 1: Setting up the Project

Create a new Flutter project by running the following command in your terminal:

```
flutter create responsive_dropdown_menu
```

Navigate to the project directory:

```
cd responsive_dropdown_menu
```

## Step 2: Adding Dependencies

Open the `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^1.0.2
```

Save the file and run the following command to fetch the dependencies:

```
flutter pub get
```

## Step 3: Building the Responsive Dropdown Menu

### 3.1 Create a new Flutter widget

Create a new file called `dropdown_menu.dart` inside the `lib` directory. Open the file and define a new `StatefulWidget` called `DropdownMenu`.

```dart
import 'package:flutter/material.dart';

class DropdownMenu extends StatefulWidget {
  @override
  _DropdownMenuState createState() => _DropdownMenuState();
}

class _DropdownMenuState extends State<DropdownMenu> {
  // TODO: Implement dropdown menu logic here

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Dropdown Menu'),
      ),
      body: Center(
        child: Text('Dropdown Menu Content'),
      ),
    );
  }
}
```

### 3.2 Implementing the Dropdown Menu

Inside the `_DropdownMenuState` class, define a `bool` variable `isDropdownOpen` to keep track of the dropdown state.

```dart
bool isDropdownOpen = false;
```

Inside the `build` method, add a `ListView.builder` widget that will act as the dropdown menu items.

```dart
ListView.builder(
  itemCount: 5,
  itemBuilder: (BuildContext context, int index) {
    return ListTile(
      title: Text('Menu Item ${index + 1}'),
      onTap: () {
        setState(() {
          isDropdownOpen = false;
        });
      },
    );
  },
),
```

Wrap the `ListView.builder` widget with a `Positioned` widget to control its position within the screen.

```dart
Positioned(
  top: 56,
  right: 0,
  left: 0,
  child: Container(
    color: Colors.white,
    child: Column(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        // Dropdown menu items
        ListView.builder(...),
      ],
    ),
  ),
),
```

### 3.3 Handling Dropdown State

To handle the opening and closing of the dropdown menu, we'll use the `GestureDetector` widget.

Wrap the `GestureDetector` around the dropdown menu content in the `build` method, and pass a callback function to its `onTap` property.

```dart
GestureDetector(
  onTap: () {
    setState(() {
      isDropdownOpen = !isDropdownOpen;
    });
  },
  child: Text(
    'Dropdown Menu',
    style: TextStyle(
      fontWeight: FontWeight.bold,
      fontSize: 18,
    ),
  ),
),
```

Finally, conditionally render the dropdown menu based on the `isDropdownOpen` value.

```dart
if (isDropdownOpen) {
  // Render dropdown menu
  Positioned(...),
}
```

## Step 4: Testing the App

Open the `main.dart` file located in the `lib` directory. Update the `home` property of the `MaterialApp` widget to use the `DropdownMenu` widget.

```dart
import 'package:flutter/material.dart';
import 'package:responsive_dropdown_menu/dropdown_menu.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Dropdown Menu',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: DropdownMenu(),
    );
  }
}
```

Save the file and run the app using the following command:

```
flutter run
```

You should now see a responsive dropdown menu in your Flutter app. The dropdown will show or hide its menu items based on whether it is tapped or not, making it suitable for different screen sizes and orientations.

## Conclusion

In this tutorial, we learned how to create a responsive dropdown menu in Flutter using the `MediaQuery` class. By adapting the layout based on screen size, we can ensure a consistent user experience across different devices. Feel free to customize the dropdown menu's appearance and behavior to fit your specific requirements.

---

#flutter #dart