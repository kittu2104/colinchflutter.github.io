---
layout: post
title: "Implementing image filters in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [imagefilters]
comments: true
share: true
---

Are you looking to add some cool image filters to your Flutter application? Whether you want to enhance the appearance of images or create unique visual effects, implementing image filters can be a great way to make your app stand out. In this blog post, we'll explore how to implement image filters in a `StatelessWidget` in Flutter.

## Getting Started

To get started, make sure you have Flutter installed on your machine. If you haven't already, you can install Flutter by following the instructions in the official Flutter documentation.

Once you have Flutter set up, create a new Flutter project and open it in your preferred code editor. We will be working with the `pubspec.yaml` file to add the required dependencies.

## Adding Dependencies

To implement image filters in Flutter, we need to add the `flutter_image_filters` package to our project. Open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_image_filters: ^0.1.0
```

Save the `pubspec.yaml` file and run the command `flutter pub get` to fetch the new dependency.

## Implementing the Image Filter

Now that we have the necessary package added to our project, let's implement an image filter. Create a new Dart file, such as `image_filter_widget.dart`, and define a `StatelessWidget` for our filter:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_image_filters/flutter_image_filters.dart';

class ImageFilterWidget extends StatelessWidget {
  final String imageUrl;

  const ImageFilterWidget({required this.imageUrl, Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return ImageFiltered(
      imageFilter: ImageFilter.blur(sigmaX: 5.0, sigmaY: 5.0),
      child: Image.network(imageUrl),
    );
  }
}
```

In the above code, we import the necessary packages, including `flutter_image_filters`. We define a `StatelessWidget` called `ImageFilterWidget`, which takes an `imageUrl` as a parameter. Inside the `build` method, we use the `ImageFiltered` widget to apply a blur image filter with a `sigmaX` and `sigmaY` of 5.0. We then display the image using the `Image.network` widget.

You can customize the image filter by changing the values of `sigmaX` and `sigmaY`. Experiment with different values to achieve the desired effect.

## Using the Image Filter Widget

To use our `ImageFilterWidget` in your Flutter application, simply create an instance of the widget and pass the `imageUrl` as a parameter. For example, you can include it in your `build` method as follows:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(title: Text('Image Filter Example')),
    body: ImageFilterWidget(imageUrl: 'https://example.com/image.jpg'),
  );
}
```

Replace `https://example.com/image.jpg` with the URL of the image you want to apply the filter to.

## Conclusion

In this blog post, we explored how to implement image filters in a `StatelessWidget` in Flutter. By leveraging the `flutter_image_filters` package, we were able to add a blur image filter to an image. Experiment with different filters and parameters to create the desired visual effects in your Flutter application.

#flutter #imagefilters