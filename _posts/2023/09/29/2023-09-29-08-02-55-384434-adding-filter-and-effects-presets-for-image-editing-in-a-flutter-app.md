---
layout: post
title: "Adding filter and effects presets for image editing in a Flutter app"
description: " "
date: 2023-09-29
tags: [imageediting, filters, effects]
comments: true
share: true
---

In today's digital world, image editing has become an essential part of our lives. Whether it's enhancing a photo or adding creative effects, having the ability to edit images right in your Flutter app can be a game-changer. One way to achieve this is by incorporating filter and effects presets.

In this tutorial, we will explore how to add filter and effects presets to an image editing feature in a Flutter app.

## Step 1: Set Up the Project

Before we start, make sure you have Flutter installed on your system. If not, you can download and install it from the official Flutter website.

Once Flutter is set up, create a new Flutter project using the following command in your terminal:

```shell
flutter create image_editor_app
```

Navigate to the project directory:

```shell
cd image_editor_app
```

## Step 2: Add Image Editing Library

To add image editing capabilities to your Flutter app, we can utilize the `image_editor` library. Open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  
  image_editor:
```

Save the file and run the following command to fetch the library:

```shell
flutter pub get
```

## Step 3: Design the Image Editor UI

Now, let's create a basic UI for the image editor. Open the `lib/main.dart` file and replace the default content with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(ImageEditorApp());
}

class ImageEditorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Image Editor',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ImageEditorScreen(),
    );
  }
}

class ImageEditorScreen extends StatefulWidget {
  @override
  _ImageEditorScreenState createState() => _ImageEditorScreenState();
}

class _ImageEditorScreenState extends State<ImageEditorScreen> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Editor'),
      ),
      body: Container(
        child: Center(
          child: Text('Image Editor Screen'),
        ),
      ),
    );
  }
}
```

This code sets up the basic structure of the app with a simple `ImageEditorScreen` widget.

## Step 4: Add Filter and Effects Presets

To add filter and effects presets, we can utilize the `image_editor` library. We first need to import it into our `lib/main.dart` file:

```dart
import 'package:image_editor/image_editor.dart';
```

Next, let's create a method that will apply a filter or effect to the image. Add the following code inside the `_ImageEditorScreenState` class:

```dart
void applyFilter(Filter filter) {
  // Apply the selected filter to the image
}

void applyEffect(Effect effect) {
  // Apply the selected effect to the image
}
```

In these methods, you can use the `filter` and `effect` objects to apply the desired modifications to the image.

## Step 5: Display Filter and Effects Presets

To provide a user-friendly interface for selecting filter and effects presets, we can use a ListView or GridView. We will populate it with the available presets and apply the selected one when tapped.

Add the following code inside the `_ImageEditorScreenState` class:

```dart
List<Filter> filters = [
  Filter(name: 'Black and White', id: 1),
  Filter(name: 'Vintage', id: 2),
  Filter(name: 'Sepia', id: 3),
];

List<Effect> effects = [
  Effect(name: 'Blur', id: 1),
  Effect(name: 'Sharpen', id: 2),
  Effect(name: 'Vignette', id: 3),
];

Widget buildFiltersPresets() {
  return ListView.builder(
    scrollDirection: Axis.horizontal,
    itemCount: filters.length,
    itemBuilder: (BuildContext context, int index) {
      Filter filter = filters[index];
      return GestureDetector(
        onTap: () => applyFilter(filter),
        child: Container(
          child: Text(filter.name),
        ),
      );
    },
  );
}

Widget buildEffectsPresets() {
  return GridView.count(
    crossAxisCount: 2,
    children: effects.map((effect) {
      return GestureDetector(
        onTap: () => applyEffect(effect),
        child: Container(
          child: Text(effect.name),
        ),
      );
    }).toList(),
  );
}
```

In this code, we have defined sample filters and effects presets. You can customize the list with your desired presets. The `buildFiltersPresets()` method builds a horizontal scrollable list of filters, while `buildEffectsPresets()` creates a grid of effects presets.

## Step 6: Integrate Presets into UI

Finally, let's integrate the presets into our app's UI. Replace the `Container` widget in the `body` property of the `Scaffold` widget inside the `_ImageEditorScreenState` class with the following code:

```dart
Column(
  children: [
    Text('Filters'),
    SizedBox(height: 10),
    buildFiltersPresets(),
    SizedBox(height: 20),
    Text('Effects'),
    SizedBox(height: 10),
    buildEffectsPresets(),
  ],
),
```

This code adds the filter and effects presets to the UI, showing the respective titles and the list/grid of presets below.

Congratulations! You have successfully implemented filter and effects presets for image editing in your Flutter app.

By providing these presets, your users will have a convenient way to enhance their images and apply creative effects without the need for complex manual editing.

#flutter #imageediting #filters #effects