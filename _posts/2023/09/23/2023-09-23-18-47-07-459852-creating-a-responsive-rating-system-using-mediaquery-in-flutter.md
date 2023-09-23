---
layout: post
title: "Creating a responsive rating system using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [flutter, ratingSystem]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive rating system using the `MediaQuery` class in Flutter. The rating system will adjust its layout based on the screen size of the device, ensuring a seamless user experience across different devices.

To get started, let's create a new Flutter project and navigate into its directory:

```shell
flutter create rating_system
cd rating_system
```

Next, open the `lib/main.dart` file in your preferred text editor and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(RatingSystemApp());
}

class RatingSystemApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Rating System',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: RatingPage(),
    );
  }
}

class RatingPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Rating System'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Icon(Icons.star, size: _getStarSize(context)),
            SizedBox(height: 8.0),
            Text('Rate this app', style: TextStyle(fontWeight: FontWeight.bold)),
          ],
        ),
      ),
    );
  }

  double _getStarSize(BuildContext context) {
    final double screenWidth = MediaQuery.of(context).size.width;

    if (screenWidth >= 600) {
      return 48.0;
    } else if (screenWidth >= 400) {
      return 36.0;
    } else {
      return 24.0;
    }
  }
}
```

In the code above, we defined a `RatingSystemApp` class responsible for creating our Flutter app. It sets the app's title, theme, and home page. The home page is defined within the `RatingPage` class, which displays the rating system.

Inside the `RatingPage` widget, we used `Column` to vertically center the `Icon` and `Text` widgets. We then used the `MediaQuery` class to retrieve the screen width and dynamically adjust the size of the `Icon` widget, depending on the screen size.

The `_getStarSize` method calculates the appropriate star size by comparing the screen width to predefined breakpoints. For screens wider than 600 pixels, the size is set to 48.0; for screens between 400 and 600 pixels, the size is set to 36.0; otherwise, it defaults to 24.0.

To run the app, use the following command in the terminal:

```shell
flutter run
```

Now you have a responsive rating system that adapts to different devices. Test it on various screen sizes and see how the star size adjusts accordingly.

That's it! You have successfully created a responsive rating system using `MediaQuery` in Flutter. Feel free to customize the design and functionality according to your requirements.

#flutter #ratingSystem