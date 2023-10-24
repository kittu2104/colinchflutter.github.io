---
layout: post
title: "Cupertino switch colors in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [material, cupertino]
comments: true
share: true
---

When developing a mobile application using Flutter, you have the option to choose between two main widget libraries: `Material` and `Cupertino`. The `Material` library provides widgets with a more modern, sleek appearance, while the `Cupertino` library offers widgets that closely resemble the iOS design. One visual difference between the two libraries is the color scheme used for switches.

## Switch Colors in MaterialApp

When using the `Material` library, switches are styled with the default Material design colors. The switch thumb (the circular button that moves when toggling the switch) has a primary color, such as green or blue, while the track (the background behind the thumb) typically has a lighter version of the primary color.

To change the colors of the switches in a `MaterialApp`, you can define a custom theme and override the default colors. Here's an example of how you can do this:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    theme: ThemeData(
      toggleableActiveColor: Colors.red, // Set the thumb color
      toggleButtonsTheme: ToggleButtonsThemeData(
        fillColor: Colors.green, // Set the track color
      ),
    ),
    home: MyHomePage(),
  ));
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Material App"),
      ),
      body: Center(
        child: Switch(
          value: true,
          onChanged: (bool newValue) {},
        ),
      ),
    );
  }
}
```

In the above code, we are setting the `toggleableActiveColor` to red, which changes the color of the switch thumb to red. Additionally, we are setting the `fillColor` of `ToggleButtonsThemeData` to green, which changes the color of the switch track to green.

## Switch Colors in CupertinoApp

When using the `Cupertino` library, switches have a distinct appearance that aligns with the iOS design guidelines. The switch thumb has a circular shape and a default light gray color, while the track is transparent.

To change the colors of `Cupertino` switches, you can customize the appearance of the `CupertinoSwitch` widget using the `activeColor` property for the thumb color and the `trackColor` property for the track color. Here's an example:

```dart
import 'package:flutter/cupertino.dart';

void main() {
  runApp(CupertinoApp(
    home: MyHomePage(),
  ));
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Cupertino App'),
      ),
      child: Center(
        child: CupertinoSwitch(
          value: true,
          onChanged: (bool newValue) {},
          activeColor: CupertinoColors.systemBlue, // Set the thumb color
          trackColor: CupertinoColors.systemGray, // Set the track color
        ),
      ),
    );
  }
}
```

In this code, we are setting the `activeColor` of the `CupertinoSwitch` widget to `CupertinoColors.systemBlue`, which changes the color of the switch thumb to a blue shade. Additionally, we are setting the `trackColor` to `CupertinoColors.systemGray`, which changes the color of the switch track to a light gray shade.

## Conclusion

The `Material` and `Cupertino` libraries in Flutter offer different switch color schemes. In a `MaterialApp`, you can customize the switch colors by defining a custom theme. On the other hand, in a `CupertinoApp`, you can directly specify the thumb and track colors using the `activeColor` and `trackColor` properties of the `CupertinoSwitch` widget.

[Flutter Material Showcase](https://flutter.dev/docs/development/ui/widgets/material)  
[Flutter Cupertino Showcase](https://flutter.dev/docs/development/ui/widgets/cupertino)  
[Flutter ThemeData class](https://api.flutter.dev/flutter/material/ThemeData-class.html)  
[Flutter CupertinoColors class](https://api.flutter.dev/flutter/cupertino/CupertinoColors-class.html)  

#flutter #material #cupertino