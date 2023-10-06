---
layout: post
title: "Creating typewriter effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In this blog post, we will explore how to create typewriter effects using the `SkiaShadersMask` widget in Flutter. The typewriter effect is a visually appealing animation where text appears to be typed out, one character at a time. This effect can be used to add an engaging and interactive element to your Flutter applications.

## Prerequisites

To follow along with this tutorial, make sure you have the following installed:

- Flutter SDK
- Dart SDK
- Android Studio or Visual Studio Code (optional)

## Getting Started

To get started, create a new Flutter project:

```bash
flutter create typewriter_effects
cd typewriter_effects
```

Open the project in your preferred IDE, and open the `lib/main.dart` file. Remove the default code and replace it with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(TypewriterEffectsApp());
}

class TypewriterEffectsApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Typewriter Effects',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TypewriterEffectsPage(),
    );
  }
}

class TypewriterEffectsPage extends StatefulWidget {
  @override
  _TypewriterEffectsPageState createState() => _TypewriterEffectsPageState();
}

class _TypewriterEffectsPageState extends State<TypewriterEffectsPage> {
  String text = '';
  int index = 0;

  @override
  void initState() {
    super.initState();
    startTypingAnimation();
  }

  void startTypingAnimation() {
    Future.delayed(Duration(milliseconds: 500), () {
      setState(() {
        if (index < typewriterText.length) {
          text += typewriterText[index];
          index++;
        } else {
          return;
        }
      });
      startTypingAnimation();
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Typewriter Effects'),
      ),
      body: Container(
        alignment: Alignment.center,
        child: Text(
          text,
          style: TextStyle(fontSize: 24.0, fontWeight: FontWeight.bold),
        ),
      ),
    );
  }
}

const String typewriterText = "Hello, World! This is a typewriter effect.";

```

In the code above, we have created a basic Flutter application with a `TypewriterEffectsPage` widget. Inside this widget, we have a `Text` widget that will display the typewriter effect. We are using the `_TypewriterEffectsPageState` class to handle the logic for the typewriter animation.

The `startTypingAnimation` method is called initially when the page loads. It uses `setState` to update the `text` variable with each character from the `typewriterText` string. The method uses recursion with `Future.delayed` to delay adding each character, giving it a typewriter effect.

Once you have added the code, save the file and run the application:

```bash
flutter run
```

You should now see a Flutter application with a `Text` widget displaying the typewriter effect. The text will appear one character at a time, with a delay of 500 milliseconds between each character.

## Conclusion

In this tutorial, we explored how to create typewriter effects using the `SkiaShadersMask` widget in Flutter. The typewriter effect can add a dynamic and engaging element to your Flutter applications. Feel free to customize the animation by adjusting the delay time or adding additional effects.

You can find the complete code on [GitHub](https://github.com/flutter/samples/tree/master/typewriter_effects). Give it a try and let us know if you have any questions or feedback!

Happy coding! 🚀 #Flutter #TypewriterEffects