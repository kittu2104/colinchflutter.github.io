---
layout: post
title: "Using SVG to create custom navigation menus in Flutter"
description: " "
date: 2023-10-31
tags: []
comments: true
share: true
---

In this blog post, we will explore how to use SVG (Scalable Vector Graphics) to create custom navigation menus in Flutter. The SVG format allows us to create scalable and flexible graphics, which is ideal for creating customized navigation menus.

## Table of Contents
- [Introduction to SVG](#introduction-to-svg)
- [Setting up the project](#setting-up-the-project)
- [Adding SVG package](#adding-svg-package)
- [Creating SVG navigation menu](#creating-svg-navigation-menu)
- [Handling menu selection](#handling-menu-selection)
- [Conclusion](#conclusion)

## Introduction to SVG

Scalable Vector Graphics (SVG) is an XML-based vector image format that supports interactivity and animation. It can be used to create 2D graphics, icons, and illustrations that can be easily resized and manipulated without losing quality.

## Setting up the project

To get started, create a new Flutter project using the following command:

```bash
flutter create svg_navigation_menu
```

Change to the project directory:

```bash
cd svg_navigation_menu
```

## Adding SVG package

To use SVG in Flutter, we need to add the `flutter_svg` package to our project. Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter_svg: ^1.0.0
```

Save the file and run the following command to fetch the package:

```bash
flutter pub get
```

## Creating SVG navigation menu

In the `lib` directory, create a new `widgets` directory. Inside this directory, create a new file called `svg_menu.dart`. This file will contain our custom SVG navigation menu widget code.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_svg/flutter_svg.dart';

class SvgMenu extends StatefulWidget {
  @override
  _SvgMenuState createState() => _SvgMenuState();
}

class _SvgMenuState extends State<SvgMenu> {
  int _selectedIndex = 0;

  List<String> _menuItems = [
    'home.svg',
    'messages.svg',
    'notifications.svg',
    'settings.svg',
  ];

  @override
  Widget build(BuildContext context) {
    return Row(
      children: List.generate(
        _menuItems.length,
        (index) => GestureDetector(
          onTap: () {
            setState(() {
              _selectedIndex = index;
            });
          },
          child: Container(
            padding: EdgeInsets.all(10),
            color: _selectedIndex == index ? Colors.blue : Colors.transparent,
            child: SvgPicture.asset(
              'assets/svg/${_menuItems[index]}',
              width: 24,
              height: 24,
              color: _selectedIndex == index ? Colors.white : Colors.black,
            ),
          ),
        ),
      ),
    );
  }
}
```

In the `_menuItems` list, we have hardcoded the names of our SVG files. Make sure to place the SVG files in the `assets/svg` directory of your project.

## Handling menu selection

To handle the menu item selection, we have used a `GestureDetector` inside the `ListView.builder`. When a menu item is tapped, it will update the `_selectedIndex` state variable. Based on this variable, we change the background color and icon color of the selected menu item.

## Conclusion

In this blog post, we have learned how to use SVG to create custom navigation menus in Flutter. By leveraging SVG's flexibility and scalability, we can create visually appealing navigation menus that seamlessly integrate into our Flutter applications.

Make sure to check out the official documentation of [flutter_svg](https://pub.dev/packages/flutter_svg) package for more advanced usage and customization options.

#flutter #SVG