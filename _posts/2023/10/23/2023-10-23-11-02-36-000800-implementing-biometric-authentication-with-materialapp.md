---
layout: post
title: "Implementing biometric authentication with MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In today's digital world, security and privacy are of utmost importance. One way to enhance the security of your mobile application is by implementing biometric authentication. Biometric authentication uses unique physical or behavioral traits such as fingerprints, face recognition, or voice recognition to verify a user's identity.

In this blog post, we will explore how to implement biometric authentication in a Flutter app using the MaterialApp widget. The MaterialApp widget is the main entry point for a Flutter application, and it provides a set of common widgets, styles, and themes for your app.

## Table of Contents
- [Overview](#overview)
- [Setting Up the Project](#setting-up-the-project)
- [Adding Biometric Authentication](#adding-biometric-authentication)
- [Handling Biometric Authentication](#handling-biometric-authentication)
- [Conclusion](#conclusion)

## Overview

Biometric authentication is an effective way to add an extra layer of security to your mobile application. By using the MaterialApp widget, we can easily implement biometric authentication in our Flutter app.

## Setting Up the Project

To get started, make sure you have Flutter installed on your machine. Create a new Flutter project by running the following command:

```bash
flutter create biometric_authentication_app
```

Once the project is created, navigate to the project directory:

```bash
cd biometric_authentication_app
```

Open the project in your favorite code editor and replace the contents of the `lib/main.dart` file with the following code:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Biometric Authentication',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Biometric Authentication'),
      ),
      body: Center(
        child: Text(
          'Implement Biometric Authentication here',
          style: TextStyle(fontSize: 20),
        ),
      ),
    );
  }
}
```

This code sets up a basic MaterialApp widget with a MyHomePage widget as the home page.

## Adding Biometric Authentication

Now that we have our project set up, let's add biometric authentication. For the purpose of this example, we will use the `local_auth` package, which provides a simple way to implement biometric authentication in Flutter.

Add the `local_auth` package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  local_auth: ^1.1.6
```

Run the following command to download the package:

```bash
flutter pub get
```

Next, update the code in the `lib/main.dart` file as follows:

```dart
import 'package:flutter/material.dart';
import 'package:local_auth/local_auth.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Biometric Authentication',
      theme: ThemeData(
        primarySwatch: Colors.blue,
        visualDensity: VisualDensity.adaptivePlatformDensity,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  final LocalAuthentication _localAuthentication = LocalAuthentication();

  Future<void> _authenticate() async {
    bool authenticated = false;
    try {
      authenticated = await _localAuthentication.authenticate(
        localizedReason: 'Authenticate to access the app',
        useErrorDialogs: true,
        stickyAuth: true,
      );
    } catch (e) {
      print(e);
    }

    if (authenticated) {
      // User authenticated, do something
    } else {
      // User not authenticated, handle accordingly
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Biometric Authentication'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Implement Biometric Authentication here',
              style: TextStyle(fontSize: 20),
            ),
            RaisedButton(
              onPressed: _authenticate,
              child: Text('Authenticate'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In this update, we added the `local_auth` import statement and the `_authenticate` method. The `_authenticate` method uses the `LocalAuthentication` class to initiate the biometric authentication process. The result of the authentication is stored in the `authenticated` variable.

## Handling Biometric Authentication

Now that we have implemented biometric authentication, we can handle the authentication result according to our needs. In the `_authenticate` method, we have provided placeholders to handle authenticated and non-authenticated states. Depending on the result, you can redirect the user to a specific page or show an error message.

It's important to handle errors and exceptions that can occur during the biometric authentication process. The `catch` block in the `_authenticate` method will catch any exceptions and print them to the console. You can modify this block to display a user-friendly error message.

## Conclusion

Implementing biometric authentication with MaterialApp is a straightforward way to enhance the security of your Flutter app. By using the `local_auth` package, we were able to add biometric authentication with just a few lines of code. Remember to handle the authentication result and any potential errors that may occur during the process.

By providing a seamless and secure authentication experience, you can boost user trust and confidence in your app. Consider implementing biometric authentication to provide your users with an added layer of security.