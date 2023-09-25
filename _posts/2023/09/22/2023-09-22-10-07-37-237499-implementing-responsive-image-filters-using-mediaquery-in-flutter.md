---
layout: post
title: "Implementing responsive image filters using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [ImageFilters]
comments: true
share: true
---

In modern app design, **image filters** have become an essential part of creating visually engaging user interfaces. Applying filters can enhance the appearance of images and make your app more visually appealing. Flutter, being a versatile UI toolkit, provides straightforward ways to implement responsive image filters using `MediaQuery`.

## What is MediaQuery?

`MediaQuery` is a class in Flutter that provides information about the user's device and app's environment. It allows you to access the device's dimensions, orientation, pixel density, and other useful properties. By leveraging MediaQuery, you can make your app responsive to various devices and screen sizes.

## Implementing Responsive Image Filters

To implement responsive image filters in Flutter, follow these steps:

1. **Import the necessary packages**:
   
   ```dart
   import 'package:flutter/material.dart';
   ```

2. **Create a StatefulWidget**:
   
   ```dart
   class ImageFilterApp extends StatefulWidget {
     @override
     _ImageFilterAppState createState() => _ImageFilterAppState();
   }
   ```

3. **Create the State class**:
   
   ```dart
   class _ImageFilterAppState extends State<ImageFilterApp> {
     @override
     Widget build(BuildContext context) {
       return MaterialApp(
         home: Scaffold(
           appBar: AppBar(
             title: const Text('Responsive Image Filters'),
           ),
           body: Center(
             child: Column(
               mainAxisAlignment: MainAxisAlignment.center,
               children: [
                 // Add your image widget here
                 // with necessary filter properties
                 ImageFiltered(
                   imageFilter: _getImageFilter(),
                   child: Image.asset('assets/images/sample_image.jpg'),
                 ),
               ],
             ),
           ),
         ),
       );
     }

     // Method to define the image filter based on device properties
     ImageFilter _getImageFilter() {
       final mediaQuery = MediaQuery.of(context);
       if (mediaQuery.platformBrightness == Brightness.dark) {
         // Apply a dark filter to the image
         return ColorFilter.matrix(<double>[
           -1, 0, 0, 0, 255,
           0, -1, 0, 0, 255,
           0, 0, -1, 0, 255,
           0, 0, 0, 1, 0,
         ]);
       } else {
         // No filter applied
         return ColorFilter.mode(Colors.transparent, BlendMode.src);
       }
     }
   }
   ```

4. **Initialize the app**:
   
   ```dart
   void main() {
     runApp(ImageFilterApp());
   }
   ```

## Explanation

In the above example, we create a `StatefulWidget` called `ImageFilterApp` and define its associated `State` class, `_ImageFilterAppState`. Inside the `build` method, we create a `Scaffold` widget and set its `body` to a `Center` widget with a column as its child.

Inside the column, we use the `ImageFiltered` widget to apply the image filter to the image. The `imageFilter` property of `ImageFiltered` receives the value from the `_getImageFilter()` method that determines the appropriate filter based on the device's properties.

In the `_getImageFilter()` method, we access the `MediaQuery` object using `MediaQuery.of(context)` and check the `platformBrightness` property. If the device is in dark mode, we apply the dark filter using the `ColorFilter.matrix()` method. Otherwise, we use `ColorFilter.mode()` to set the filter to transparent, indicating no filter is applied.

By dynamically applying image filters based on device properties, you can create responsive and visually appealing applications using Flutter.

That's it! You have successfully implemented responsive image filters using `MediaQuery` in Flutter. Experiment and customize the image filters to suit your app's design and requirements. Happy coding!

## #Flutter #ImageFilters