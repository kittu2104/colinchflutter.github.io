---
layout: post
title: "Implementing custom fonts in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: [Flutter, CustomFonts]
comments: true
share: true
---

Step 1: Add Custom Fonts to Your Project

Before we can use custom fonts in our app, we need to add the font files to our project. To do this, follow these steps:

1. Create a new directory in the root of your Flutter project and name it 'assets'. This is where you will store all your font files.
2. Copy the font file(s) (.ttf or .otf) into the 'assets' directory. Make sure you have the appropriate license or permission to use the font files.
3. Open the 'pubspec.yaml' file in your Flutter project.
4. Find the 'flutter' section and add the following code snippet to specify the path to your font files:

```
flutter:
  fonts:
    - family: MyCustomFont
      fonts:
        - asset: assets/font_file.ttf
```

Replace `assets/font_file.ttf` with the actual path to your font file.

Step 2: Load the Custom Font

Now that we've added our custom font to the project, we can load it into our app. In your StatelessWidget, follow these steps to load the font:

1. Import the `flutter/services.dart` package.
2. Add the following code snippet inside your StatelessWidget class:

```
import 'package:flutter/services.dart';

class MyCustomWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Load the font
    final fontLoader = FontLoader('MyCustomFont');
    fontLoader.addFont(rootBundle.load('assets/font_file.ttf'));

    return FutureBuilder(
      future: fontLoader.load(),
      builder: (BuildContext context, AsyncSnapshot<void> snapshot) {
        if (snapshot.connectionState == ConnectionState.done) {
          // Font has been loaded, build your UI here
          return Text(
            'Hello World',
            style: TextStyle(
              fontFamily: 'MyCustomFont',
            ),
          );
        } else {
          // Font is still loading, show a loader or fallback UI
          return CircularProgressIndicator();
        }
      },
    );
  }
}
```

Replace `'MyCustomFont'` in the `fontLoader` and `TextStyle` with the actual font family name specified in the 'pubspec.yaml' file.

Step 3: Using the Custom Font

Now that we have loaded the custom font, we can use it in our UI. In this example, we use the custom font for a `Text` widget, but you can apply it to any other widget that supports a `TextStyle`. 

```
Text(
  'Hello Flutter',
  style: TextStyle(
    fontFamily: 'MyCustomFont',
    fontSize: 24,
  ),
)
```

Remember to replace `'MyCustomFont'` with the actual font family name from the 'pubspec.yaml' file. Adjust the `fontSize` and other properties to your liking.

Conclusion

Implementing custom fonts in a StatelessWidget in Flutter is straightforward. By adding the font files to your project, loading the font, and using it in your UI, you can easily give your app a unique and personalized touch. Custom fonts are a great way to enhance the visual appeal of your Flutter app and create a consistent brand experience for your users.

#Flutter #CustomFonts