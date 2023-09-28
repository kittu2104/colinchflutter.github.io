---
layout: post
title: "Creating a responsive login form using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [responsive]
comments: true
share: true
---

![flutter-logo](https://example.com/flutter-logo.png)

Creating a responsive user interface is crucial when designing mobile applications. In Flutter, you can achieve this using `MediaQuery` to adapt your UI based on the available device screen size. In this tutorial, we will create a responsive login form that adjusts its layout based on the device screen size.

## Step 1: Set up a new Flutter project

Before diving into the code, make sure you have Flutter installed on your machine. If not, follow the official Flutter installation guide to get started.

To create a new Flutter project, run the following command:

```bash
flutter create responsive_login_form
```

## Step 2: Designing the login form

Open the `lib/main.dart` file in your project. This file will contain the main entry point of the application. Replace the default code with the following Flutter code snippet:

```dart
import 'package:flutter/material.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Login Form',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: LoginPage(),
    );
  }
}

class LoginPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Login'),
      ),
      body: Center(
        child: Container(
          padding: EdgeInsets.all(16),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              TextField(
                decoration: InputDecoration(
                  labelText: 'Username',
                  border: OutlineInputBorder(),
                ),
              ),
              SizedBox(height: 16),
              TextField(
                decoration: InputDecoration(
                  labelText: 'Password',
                  border: OutlineInputBorder(),
                ),
                obscureText: true,
              ),
              SizedBox(height: 16),
              RaisedButton(
                onPressed: () {},
                child: Text('Login'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

In the code snippet above, we have defined a simple login form using Flutter's `Scaffold` widget. The form contains two `TextField` widgets for username and password input, and a `RaisedButton` for the login action. We have also added some basic styling to the form using Flutter's `Theme` and `AppBar` widgets.

## Step 3: Making the login form responsive

Now that our login form is complete, we can make it responsive using `MediaQuery`. Modify the `LoginPage` class as follows:

```dart
class LoginPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;

    return Scaffold(
      appBar: AppBar(
        title: Text('Login'),
      ),
      body: Center(
        child: Container(
          padding: EdgeInsets.all(16),
          constraints: BoxConstraints(
            maxWidth: 400,
          ),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              if (screenWidth < 600) ...[
                TextField(
                  decoration: InputDecoration(
                    labelText: 'Username',
                    border: OutlineInputBorder(),
                  ),
                ),
                SizedBox(height: 16),
              ],
              TextField(
                decoration: InputDecoration(
                  labelText: 'Password',
                  border: OutlineInputBorder(),
                ),
                obscureText: true,
              ),
              SizedBox(height: 16),
              RaisedButton(
                onPressed: () {},
                child: Text('Login'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

In this modified code, we have added a `final screenWidth` variable to store the screen width obtained from `MediaQuery.of(context).size.width`. We then make the login form responsive by wrapping the relevant parts of the UI within an `if` condition that checks the screen width.

In this example, if the screen width is less than 600 (which can be considered a phone-sized screen), we display the username text field. If the screen width is equal to or greater than 600 (e.g., a tablet or desktop-sized screen), the username field is not displayed.

By using `MediaQuery` and conditional rendering, our login form now adapts to different screen sizes, providing an optimized user experience across various devices.

## Conclusion

In this tutorial, we have learned how to create a responsive login form using `MediaQuery` in Flutter. By incorporating `MediaQuery` into our UI code, we can dynamically adjust the layout and content based on the available screen size. This approach allows us to create user-friendly applications that work well on different devices.

#flutter #responsive-design