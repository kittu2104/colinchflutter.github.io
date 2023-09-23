---
layout: post
title: "Creating a responsive login form using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [flutter, loginform, responsivedesign]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive login form in Flutter using the `MediaQuery` class. The `MediaQuery` class allows us to retrieve information about the current device's size, orientation, and other characteristics.

## Prerequisites

Before we begin, make sure you have Flutter installed on your machine. You can follow the official [Flutter installation guide](https://flutter.dev/docs/get-started/install) to set up Flutter.

## Step 1: Create a new Flutter project

Open your favorite IDE and create a new Flutter project. Run the following command in your terminal:

```bash
flutter create responsive_login_form
cd responsive_login_form
```

## Step 2: Add necessary dependencies

Open the `pubspec.yaml` file and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_screenutil: ^5.1.1
```

Save the file and run `flutter pub get` in your terminal to install the dependencies.

## Step 3: Design the login form

Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_screenutil/flutter_screenutil.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ScreenUtilInit(
      designSize: Size(360, 640),
      builder: () => MaterialApp(
        debugShowCheckedModeBanner: false,
        title: 'Responsive Login Form',
        theme: ThemeData(primarySwatch: Colors.blue),
        home: LoginPage(),
      ),
    );
  }
}

class LoginPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: SafeArea(
        child: Padding(
          padding: EdgeInsets.all(ScreenUtil().setWidth(16)),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            crossAxisAlignment: CrossAxisAlignment.stretch,
            children: [
              Text(
                'Login',
                style: TextStyle(
                  fontSize: ScreenUtil().setSp(24),
                  fontWeight: FontWeight.bold,
                ),
              ),
              SizedBox(height: ScreenUtil().setHeight(32)),
              TextField(
                decoration: InputDecoration(
                  hintText: 'Email',
                  border: OutlineInputBorder(),
                ),
              ),
              SizedBox(height: ScreenUtil().setHeight(16)),
              TextField(
                decoration: InputDecoration(
                  hintText: 'Password',
                  border: OutlineInputBorder(),
                ),
              ),
              SizedBox(height: ScreenUtil().setHeight(16)),
              ElevatedButton(
                onPressed: () {},
                child: Text('Sign In'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

In this code, we have created a basic login form with two text fields for email and password, and a sign-in button. The `ScreenUtil` class is used to make the form responsive by scaling the UI elements based on the device size.

## Step 4: Run the app

Save the file and run the app using the following command:

```bash
flutter run
```

You should now see the login form displayed on the screen. Try resizing the window or running the app on different devices to see how the form adjusts to different screen sizes.

Congratulations! You have successfully created a responsive login form using `MediaQuery` in Flutter. Feel free to customize the form and add additional functionality as per your requirements.

## Conclusion

In this tutorial, we learned how to create a responsive login form in Flutter using the `MediaQuery` class. By leveraging the `MediaQuery` class, we can create UIs that adapt well to different screen sizes and orientations. Building responsive UIs is crucial for providing a consistent user experience across multiple devices.

#flutter #loginform #responsivedesign