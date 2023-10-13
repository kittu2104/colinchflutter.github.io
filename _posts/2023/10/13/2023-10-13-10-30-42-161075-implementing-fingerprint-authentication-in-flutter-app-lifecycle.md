---
layout: post
title: "Implementing fingerprint authentication in Flutter app lifecycle"
description: " "
date: 2023-10-13
tags: [integrating, conclusion]
comments: true
share: true
---

When it comes to securing sensitive data in a Flutter app, one effective approach is to use fingerprint authentication. Fingerprint authentication provides an extra layer of security by requiring the user to authenticate using their unique fingerprint.

In this blog post, we will explore the steps required to implement fingerprint authentication in a Flutter app and integrate it into the app's lifecycle.

## **Table of Contents**
- [Getting Started](#getting-started)
- [Adding Required Dependencies](#adding-required-dependencies)
- [Implementing Fingerprint Authentication](#implementing-fingerprint-authentication)
- [Integrating with App Lifecycle](#integrating-with-app-lifecycle)
- [Conclusion](#conclusion)

## **Getting Started**{#getting-started}

Before we begin, make sure you have Flutter and Dart installed on your machine. You can download Flutter from the official Flutter website and follow the installation instructions provided.

Next, create a new Flutter project by running the following command in your terminal:

```bash
flutter create fingerprint_authentication_app
```

Change to the project directory:

```bash
cd fingerprint_authentication_app
```

Open the project in your favorite code editor.

## **Adding Required Dependencies**{#adding-required-dependencies}

To implement fingerprint authentication, we need to add the `local_auth` package to our project. Open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  local_auth: ^2.0.0
```

Save the file and run the command below to fetch the package:

```bash
flutter pub get
```

## **Implementing Fingerprint Authentication**{#implementing-fingerprint-authentication}

We can now proceed with implementing fingerprint authentication in our Flutter app. Create a new Dart file, `fingerprint_auth.dart`, and define a class named `FingerprintAuth`:

```dart
import 'package:local_auth/local_auth.dart';

class FingerprintAuth {
  final _auth = LocalAuthentication();

  Future<bool> authenticate() async {
    bool isAuthenticated = false;
    try {
      isAuthenticated = await _auth.authenticate(
        localizedReason: 'Authentication required',
        biometricOnly: true,
        useErrorDialogs: true,
      );
    } catch (e) {
      print(e);
    }
    return isAuthenticated;
  }
}
```

In this class, we import the `local_auth` package and create an instance of `LocalAuthentication`. The `authenticate` method is responsible for initiating the fingerprint authentication process. We provide a localized reason for authentication, enable biometric-only authentication (fingerprint only), and allow the use of error dialogs. The method returns a boolean indicating whether the authentication was successful or not.

## **Integrating with App Lifecycle**{#integrating-with-app-lifecycle}

To integrate fingerprint authentication with the app's lifecycle, we need to listen for app state changes and prompt the user for fingerprint authentication when the app comes back from the background to the foreground.

Open the `main.dart` file and replace the existing content with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:fingerprint_authentication_app/fingerprint_auth.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> with WidgetsBindingObserver {
  FingerprintAuth _fingerprintAuth;

  @override
  void initState() {
    super.initState();
    _fingerprintAuth = FingerprintAuth();
    WidgetsBinding.instance.addObserver(this);
  }

  @override
  void dispose() {
    WidgetsBinding.instance.removeObserver(this);
    super.dispose();
  }

  @override
  void didChangeAppLifecycleState(AppLifecycleState state) async {
    if (state == AppLifecycleState.resumed) {
      final isAuthenticated = await _fingerprintAuth.authenticate();
      if (!isAuthenticated) {
        // Handle authentication failure
      }
    }
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: Text('Fingerprint Authentication')),
        body: Center(child: Text('Welcome to the app')),
      ),
    );
  }
}
```

We have made a few changes to the existing code. First, we import our `FingerprintAuth` class. We then extend `_MyAppState` with `WidgetsBindingObserver` and override the `didChangeAppLifecycleState` method. This method gets called whenever the app's lifecycle state changes. When the app resumes from the background, we call the `authenticate` method to prompt the user for fingerprint authentication. If the authentication fails, you can handle it accordingly.

Don't forget to add the necessary permissions to the AndroidManifest.xml file and Info.plist file for Android and iOS respectively.

## **Conclusion**{#conclusion}

In this blog post, we have learned how to implement fingerprint authentication in a Flutter app and integrate it with the app's lifecycle. Fingerprint authentication adds an extra layer of security to your app and helps protect sensitive user data. By following the steps outlined in this post, you can easily incorporate fingerprint authentication into your Flutter app.

Remember, proper app and data security practices go beyond just fingerprint authentication. Always ensure that you handle sensitive data securely and follow best practices recommended by security experts.

#References
- [Flutter documentation](https://flutter.dev/docs)
- [local_auth package](https://pub.dev/packages/local_auth)