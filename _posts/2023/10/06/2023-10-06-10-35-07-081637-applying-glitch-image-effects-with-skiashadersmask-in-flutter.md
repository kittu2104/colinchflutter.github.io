---
layout: post
title: "Applying glitch image effects with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

Flutter offers powerful graphics rendering capabilities through its Skia graphics engine. One interesting use case is applying glitch image effects to add some visual interest to your app. In this tutorial, we'll explore how to achieve this effect using the `SkiaShaderMask` widget.

## Table of Contents
- [What is SkiaShaderMask?](#what-is-skiashadermask)
- [Implementing the Glitch Effect](#implementing-the-glitch-effect)
- [Adding Interactivity](#adding-interactivity)
- [Conclusion](#conclusion)

## What is SkiaShaderMask?
SkiaShaderMask is a Flutter widget that allows us to apply a custom shader to a specific area of an image. A shader is essentially a set of instructions that determines how colors or patterns will be applied to a shape or image.

## Implementing the Glitch Effect
To create a glitch effect, we'll start by defining a custom shader. This shader will simulate the distortion and displacement of pixels found in glitch art.

```dart
final glitchShader = LinearGradient(
  colors: [Colors.red, Colors.green, Colors.blue],
  stops: [0.3, 0.5, 0.8],
).createShader(Rect.fromLTWH(0, 0, width, height));
```

In the above example, we create a `LinearGradient` shader with three colors and stops. Feel free to experiment with different colors and positions to achieve your desired glitch effect.

Next, we can use the `SkiaShaderMask` widget to apply the shader to an image:

```dart
SkiaShaderMask(
  shader: glitchShader,
  blendMode: BlendMode.srcATop,
  child: Image.network('https://example.com/image.jpg'),
)
```

In this code snippet, we pass our `glitchShader` to the `shader` parameter of `SkiaShaderMask`. We also specify the `BlendMode.srcATop` blend mode to control how the image and shader are combined. Finally, we use the `child` parameter to specify the image we want to apply the effect to.

## Adding Interactivity
To make the glitch effect more dynamic, we can add interactivity by using a `GestureDetector` widget. Here's an example of how we can modify our code to add interactivity:

```dart
GestureDetector(
  onPanUpdate: (details) {
    setState(() {
      // Update glitchShader parameters based on pan gesture details
    });
  },
  child: SkiaShaderMask(
    shader: glitchShader,
    blendMode: BlendMode.srcATop,
    child: Image.network('https://example.com/image.jpg'),
  ),
)
```

In this example, we wrap our `SkiaShaderMask` widget with a `GestureDetector` and listen for `onPanUpdate` events. You can then update the `glitchShader` parameters based on the pan gesture details, such as the position of the user's finger on the screen.

## Conclusion
By leveraging the Skia graphics engine in Flutter, we can easily apply glitch image effects to enhance the visual appeal of our apps. The `SkiaShaderMask` widget makes it straightforward to create custom shaders and apply them to specific areas of an image. With a bit of interactivity, you can create engaging glitch effects that respond to user input.

Give it a try and unleash your creativity with glitch art in your Flutter apps!

\#Flutter \#SkiaGraphics #GlitchEffects