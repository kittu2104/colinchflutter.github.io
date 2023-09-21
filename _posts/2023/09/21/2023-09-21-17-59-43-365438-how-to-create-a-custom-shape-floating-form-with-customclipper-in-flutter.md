---
layout: post
title: "How to create a custom shape floating form with CustomClipper in Flutter"
description: " "
date: 2023-09-21
tags: []
comments: true
share: true
---

In this tutorial, we will learn how to create a custom shape floating form using the **CustomClipper** widget in Flutter. The **CustomClipper** widget allows us to create custom shapes by clipping any widget based on a specific shape.

## Prerequisites

Before we begin, make sure you have Flutter installed on your system and have set up your development environment.

## Step 1: Adding Dependencies

First, we need to add the necessary dependencies to your **pubspec.yaml** file. Open the file and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^1.0.2
```

Save the file and run `flutter pub get` to fetch the added dependencies.

## Step 2: Creating the CustomClipper Widget

Create a new **dart** file called **custom_shape_clipper.dart** and add the following code:

```dart
import 'package:flutter/material.dart';

class CustomShapeClipper extends CustomClipper<Path> {
  @override
  Path getClip(Size size) {
    var path = Path();

    path.lineTo(0, size.height - 50);
    path.quadraticBezierTo(
        size.width / 2, size.height, size.width, size.height - 50);
    path.lineTo(size.width, 0);
    path.close();

    return path;
  }

  @override
  bool shouldReclip(CustomClipper<Path> oldClipper) => false;
}
```

In this code, we define a custom class called **CustomShapeClipper** that extends the **CustomClipper** class. We override two methods:

- `getClip`: This method is responsible for creating the custom shape by defining a series of points and curves. In our case, we are creating a flowing form shape by using straight lines and a quadratic Bezier curve.
- `shouldReclip`: This method is used to determine if the clipper should be recalculated when the widget is rebuilt.

## Step 3: Creating the Floating Form

Now, open your main.dart file and modify it as follows:

```dart
import 'package:flutter/material.dart';
import 'custom_shape_clipper.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Custom Shape Floating Form',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Custom Shape Floating Form'),
        ),
        body: Stack(
          children: [
            ClipPath(
              clipper: CustomShapeClipper(),
              child: Container(
                height: 200,
                decoration: BoxDecoration(
                  color: Colors.blue,
                ),
              ),
            ),
            Padding(
              padding: EdgeInsets.all(16.0),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.stretch,
                children: [
                  TextField(
                    decoration: InputDecoration(
                      labelText: 'Name',
                    ),
                  ),
                  SizedBox(height: 16.0),
                  TextField(
                    decoration: InputDecoration(
                      labelText: 'Email',
                    ),
                  ),
                  SizedBox(height: 16.0),
                  ElevatedButton(
                    onPressed: () {},
                    child: Text('Submit'),
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

In this code, we import the **CustomShapeClipper** class we defined earlier. We then modify the **MyApp** class to use a **Stack** widget to overlay the custom shaped form on top of a colored container. Inside the form, we include a few **TextFields** and an **ElevatedButton** widget.

## Step 4: Running the App

Save all the changes and run the app using the `flutter run` command. You should see the custom shape floating form with the provided name and email fields. 

Feel free to customize the shape and the form fields as needed to fit your project requirements.

That's it! You have successfully created a custom shape floating form using the **CustomClipper** widget in Flutter.

Happy coding!

## Conclusion

In this tutorial, we learned how to create a custom shape floating form using the **CustomClipper** widget in Flutter. We started by adding the necessary dependencies, then created a custom clipper class to define the shape. Finally, we created the floating form widget by overlaying the custom shape on top of the form components.