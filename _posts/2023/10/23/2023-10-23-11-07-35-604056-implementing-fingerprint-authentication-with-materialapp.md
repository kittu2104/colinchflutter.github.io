---
layout: post
title: "Implementing fingerprint authentication with MaterialApp."
description: " "
date: 2023-10-23
tags: [BiometricAuthentication]
comments: true
share: true
---

In today's digital world, security is of utmost importance. One way to enhance the security of an application is by implementing fingerprint authentication. By incorporating fingerprint authentication, users can securely access their sensitive information with just a touch of their finger. In this blog post, we will explore how to implement fingerprint authentication using the `MaterialApp` widget in Flutter.

## Table of Contents
- [What is fingerprint authentication](#what-is-fingerprint-authentication)
- [Setting up the project](#setting-up-the-project)
- [Implementing fingerprint authentication](#implementing-fingerprint-authentication)
- [Handling fingerprint authentication callbacks](#handling-fingerprint-authentication-callbacks)
- [Conclusion](#conclusion)

## What is fingerprint authentication

Fingerprint authentication is a biometric security feature that allows users to verify their identity by using their unique fingerprint. This technology has become increasingly popular in mobile devices due to its convenience and enhanced security.

## Setting up the project

To get started, you need to have Flutter installed on your machine. If you haven't installed Flutter yet, you can follow the official [installation guide](https://flutter.dev/docs/get-started/install) to set it up.

Once you have Flutter installed, create a new Flutter project using the following command:

```shell
flutter create fingerprint_auth
```

Navigate into the project directory:

```shell
cd fingerprint_auth
```

Open the project in your preferred code editor.

Now, let's add the necessary dependencies to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  local_auth: ^2.0.1
```

Save the file and run the following command to fetch the dependencies:

```shell
flutter pub get
```

## Implementing fingerprint authentication

To implement fingerprint authentication, we'll utilize the `local_auth` package in Flutter. This package provides a high-level interface to interact with the device's biometric authentication capabilities.

Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';
import 'package:local_auth/local_auth.dart';

void main() {
  runApp(MaterialApp(
    home: FingerprintAuthScreen(),
  ));
}

class FingerprintAuthScreen extends StatefulWidget {
  @override
  _FingerprintAuthScreenState createState() => _FingerprintAuthScreenState();
}

class _FingerprintAuthScreenState extends State<FingerprintAuthScreen> {
  final LocalAuthentication _localAuthentication = LocalAuthentication();
  bool _isBiometricAvailable = false;

  @override
  void initState() {
    super.initState();
    checkBiometricAvailability();
  }

  Future<void> checkBiometricAvailability() async {
    bool isAvailable = await _localAuthentication.canCheckBiometrics;

    setState(() {
      _isBiometricAvailable = isAvailable;
    });
  }

  Future<void> authenticateWithBiometrics() async {
    bool isAuthenticated = false;

    try {
      isAuthenticated = await _localAuthentication.authenticate(
        localizedReason: 'Authenticate to access your sensitive information',
        biometricOnly: true,
      );
    } catch (e) {
      print('Error: $e');
    }

    if (isAuthenticated) {
      // Authentication successful, proceed to the secured page
      // TODO: Implement navigation to the secured page
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Fingerprint Authentication')),
      body: Center(
        child: _isBiometricAvailable
            ? RaisedButton(
                child: Text('Authenticate with Fingerprint'),
                onPressed: authenticateWithBiometrics,
              )
            : Text('Fingerprint authentication is not supported on this device'),
      ),
    );
  }
}
```

In the code above, we have created a `FingerprintAuthScreen` widget that will be the home screen of our application. We use the `LocalAuthentication` class from the `local_auth` package to interact with the device's biometric authentication capabilities.

Inside the `FingerprintAuthScreen` class, we check the availability of biometric authentication using the `canCheckBiometrics` method. If biometric authentication is available, we display a button to authenticate with the user's fingerprint. When the button is pressed, the `_localAuthentication.authenticate` method is called to initiate the authentication process.

## Handling fingerprint authentication callbacks

To handle the result of the fingerprint authentication process, we can add a callback to the `authenticate` method. This callback is called when the authentication process is completed, whether successful or not.

You can modify the `authenticateWithBiometrics` method as follows to handle the authentication result:

```dart
...

Future<void> authenticateWithBiometrics() async {
  bool isAuthenticated = false;

  try {
    isAuthenticated = await _localAuthentication.authenticate(
      localizedReason: 'Authenticate to access your sensitive information',
      biometricOnly: true,
    );
  } catch (e) {
    print('Error: $e');
  }

  if (isAuthenticated) {
    // Authentication successful, proceed to the secured page
    // TODO: Implement navigation to the secured page
  } else {
    // Authentication failed, display an error message
    showDialog(
      context: context,
      builder: (BuildContext context) {
        return AlertDialog(
          title: Text('Authentication Failed'),
          content: Text('Please try again'),
          actions: <Widget>[
            FlatButton(
              child: Text('OK'),
              onPressed: () => Navigator.of(context).pop(),
            ),
          ],
        );
      },
    );
  }
}

...
```

In this updated code, we handle the case where authentication fails by showing an `AlertDialog` with an appropriate error message.

## Conclusion

In this blog post, we explored how to implement fingerprint authentication using the `MaterialApp` widget in Flutter. We learned how to check the availability of biometric authentication, authenticate with the user's fingerprint, and handle the authentication result. By adding fingerprint authentication to your app, you can greatly enhance the security and convenience for your users.

Remember to handle exceptions and errors appropriately when implementing biometric authentication, and always ensure to test your app thoroughly on different devices and scenarios.

Stay tuned for more Flutter tutorials and tips! #Flutter #BiometricAuthentication