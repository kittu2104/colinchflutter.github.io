---
layout: post
title: "Stepper widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [stepper]
comments: true
share: true
---

When building a cross-platform mobile application, you have the option to choose between different UI frameworks. Two popular options for building mobile apps are **MaterialApp** and **CupertinoApp**, which are provided by Flutter.

Both MaterialApp and CupertinoApp come with a wide range of widgets that you can use to create great user interfaces. In this blog post, we'll focus on the **Stepper** widget and how it differs when used in MaterialApp and CupertinoApp.

## What is the Stepper widget?

The Stepper widget is used to represent a sequence of steps in a linear or non-linear manner. It is commonly used for guiding users through complex workflows or multi-step forms. The widget displays a series of labels and optional icons indicating the step's completion status.

## MaterialApp Stepper

When using the Stepper widget in a MaterialApp, it follows the Material Design guidelines provided by Google. This means that the Stepper widget will have a Material look and feel, with a sleek and modern design.

The MaterialApp Stepper typically features:

- A vertical layout, where each step is displayed one below the other.
- A flexible and customizable design that can be easily themed to match your app's branding.
- Built-in animations and transitions for navigating between steps.

To use the Stepper widget in a MaterialApp, you can simply wrap it within a MaterialApp widget and configure the necessary properties such as the current step, steps list, and callback functions for handling user actions.

## CupertinoApp Stepper

On the other hand, when using the Stepper widget in a CupertinoApp, it adheres to the design principles of Apple's iOS platform. This means that the Stepper widget will have the familiar iOS look and feel, with its distinctive style and animations.

The CupertinoApp Stepper typically features:

- A horizontal layout, with each step displayed side by side.
- A sleek and minimalist design that aligns with iOS interface guidelines.
- Smooth animations and transitions, which are common in iOS apps.

To use the Stepper widget in a CupertinoApp, you can wrap it within a CupertinoApp widget and configure the necessary properties, similar to how it is done in a MaterialApp.

## Conclusion

Choosing between the MaterialApp Stepper and the CupertinoApp Stepper depends on the design guidelines you want to follow for your mobile application. If you aim to create a cross-platform app with a consistent look and feel across different platforms, MaterialApp may be the right choice. On the other hand, if you want to provide an iOS-native experience for your iOS users, the CupertinoApp Stepper is the way to go.

Remember, regardless of the framework you choose, Flutter provides a rich set of widgets that can be customized to suit your specific needs.

---

**References:**

- Flutter Material Design: [https://flutter.dev/docs/development/ui/widgets/material](https://flutter.dev/docs/development/ui/widgets/material)
- Flutter Cupertino Design: [https://flutter.dev/docs/development/ui/widgets/cupertino](https://flutter.dev/docs/development/ui/widgets/cupertino)

#flutter #stepper