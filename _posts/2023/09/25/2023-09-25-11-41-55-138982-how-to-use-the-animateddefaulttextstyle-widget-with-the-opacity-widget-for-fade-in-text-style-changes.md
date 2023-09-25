---
layout: post
title: "How to use the AnimatedDefaultTextStyle widget with the Opacity widget for fade-in text style changes"
description: " "
date: 2023-09-25
tags: [flutter, textstyle]
comments: true
share: true
---

In Flutter, you can create smooth and dynamic fade-in text style changes using the `AnimatedDefaultTextStyle` and `Opacity` widgets. This combination allows you to animate the transition between different text styles while controlling the opacity of the text.

Here's an example of how you can achieve this effect:

```dart
import 'package:flutter/material.dart';

class FadeInTextStyleExample extends StatefulWidget {
  @override
  _FadeInTextStyleExampleState createState() => _FadeInTextStyleExampleState();
}

class _FadeInTextStyleExampleState extends State<FadeInTextStyleExample> 
  with SingleTickerProviderStateMixin {
  
  AnimationController _controller;
  Animation<double> _opacityAnimation;
  TextStyle _currentTextStyle = TextStyle(fontSize: 20, color: Colors.blue);
  
  @override
  void initState() {
    super.initState();
    
    _controller = AnimationController(
      duration: Duration(seconds: 2),
      vsync: this,
    );
    
    _opacityAnimation = Tween<double>(begin: 0, end: 1).animate(_controller);
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }
  
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Fade-In Text Style'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            AnimatedDefaultTextStyle(
              style: _currentTextStyle,
              duration: Duration(seconds: 1),
              child: Opacity(
                opacity: _opacityAnimation.value,
                child: Text('Hello World'),
              ),
            ),
            SizedBox(height: 10),
            RaisedButton(
              child: Text('Change Style'),
              onPressed: () {
                setState(() {
                  _currentTextStyle = TextStyle(fontSize: 30, color: Colors.red);
                });
                _controller.forward();
              },
            ),
          ],
        ),
      ),
    );
  }
}
```

In this example, we start with a `TextStyle` of `fontSize: 20` and `color: Colors.blue`. The `AnimatedDefaultTextStyle` widget allows us to smoothly transition to a new style when it changes within the specified duration. In this case, we animate the transition over 1 second.

The `Opacity` widget is used to control the opacity of the text. The `Opacity` widget takes an `opacity` property, which is controlled by the `_opacityAnimation` value. We define a `Tween` to smoothly transition the opacity value from 0 to 1 over the duration of the animation.

To trigger the style change and animation, we use a `RaisedButton`. When pressed, it updates the `_currentTextStyle` to `fontSize: 30` and `color: Colors.red`, and then starts the animation by calling `_controller.forward()`.

By combining `AnimatedDefaultTextStyle` and `Opacity` widgets, you can create fade-in text style changes to enhance the user experience in your Flutter applications.

#flutter #textstyle #animation