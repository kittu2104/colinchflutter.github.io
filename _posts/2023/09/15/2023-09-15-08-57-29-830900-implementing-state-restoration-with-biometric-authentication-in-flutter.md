---
layout: post
title: "Implementing state restoration with biometric authentication in Flutter"
description: " "
date: 2023-09-15
tags: []
comments: true
share: true
---

In today's world, security is of utmost importance, especially when it comes to protecting sensitive user data in your Flutter applications. One powerful security feature that you can implement is biometric authentication. This not only provides a seamless user experience but also adds an extra layer of protection to your app.

But what happens when the user closes the app and comes back later? They would expect to be logged in automatically if they have already authenticated with their biometrics, right? This is where state restoration comes into play.

State restoration allows you to save and restore the state of your app, including authentication data, so that users don't have to go through the authentication process again each time they open the app. Let's see how we can achieve this in Flutter.

## Setting up the Project

First, create a new Flutter project or navigate to your existing Flutter project.

```dart
flutter create biometric_auth_flutter
cd biometric_auth_flutter
```

## Adding Dependencies

To implement biometric authentication and state restoration, we need to add the following dependencies to our `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter

  local_auth: ^2.0.0
  shared_preferences: ^2.0.5
  flutter_secure_storage: ^4.2.0
```

- `local_auth` allows us to authenticate the user using their device's biometrics.
- `shared_preferences` is used to save and retrieve the authentication state.
- `flutter_secure_storage` securely stores authentication data.

After adding the dependencies, run `flutter pub get` to fetch them.

## Implementing Biometric Authentication

To implement biometric authentication, we'll create a `BiometricAuth` class. Inside this class, we'll use the `local_auth` package to authenticate the user using their biometrics.

```dart
import 'package:local_auth/local_auth.dart';

class BiometricAuth {
  final LocalAuthentication _localAuthentication = LocalAuthentication();

  Future<bool> authenticate() async {
    try {
      return await _localAuthentication.authenticate(
        biometricOnly: true,
        localizedReason: 'Authenticate to access your data',
        useErrorDialogs: true,
        stickyAuth: true,
      );
    } catch (e) {
      print('Authentication Error: $e');
      return false;
    }
  }
}
```

In the `authenticate()` method, we provide a localized reason for authentication and set `biometricOnly` to `true` to ensure only biometrics are used for authentication.

## Saving and Restoring Authentication State

To save and restore the authentication state using `shared_preferences` and `flutter_secure_storage`, we'll create a `AuthStateManager` class. This class will have two methods: `saveAuthenticationState()` and `restoreAuthenticationState()`.

```dart
import 'package:shared_preferences/shared_preferences.dart';
import 'package:flutter_secure_storage/flutter_secure_storage.dart';

class AuthStateManager {
  final SharedPreferences _sharedPreferences;
  final FlutterSecureStorage _secureStorage;

  AuthStateManager(this._sharedPreferences, this._secureStorage);

  Future<void> saveAuthenticationState(bool isAuthenticated) async {
    await _sharedPreferences.setBool('isAuthenticated', isAuthenticated);
  }

  Future<bool> restoreAuthenticationState() async {
    final isAuthenticated = _sharedPreferences.getBool('isAuthenticated') ?? false;

    final hasBiometrics = await _secureStorage.containsKey(key: 'biometricKey');

    return isAuthenticated && hasBiometrics;
  }
}
```

In the `saveAuthenticationState()` method, we save the authentication state using a `SharedPreferences` instance. In the `restoreAuthenticationState()` method, we check if the user is authenticated and if biometrics data is available using `FlutterSecureStorage`.

## Using Biometric Authentication and State Restoration

To utilize the `BiometricAuth` and `AuthStateManager` classes in our app, we'll create a simple login screen where the user can authenticate using their biometrics.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(BiometricAuthApp());
}

class BiometricAuthApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(title: const Text('Biometric Auth')),
        body: Center(
          child: ElevatedButton(
            onPressed: () {
              authenticateWithBiometrics();
            },
            child: const Text('Authenticate with Biometrics'),
          ),
        ),
      ),
    );
  }

  Future<void> authenticateWithBiometrics() async {
    final biometricAuth = BiometricAuth();
    final authStateManager = AuthStateManager(
      await SharedPreferences.getInstance(),
      FlutterSecureStorage(),
    );

    final isAuthenticated = await biometricAuth.authenticate();

    await authStateManager.saveAuthenticationState(isAuthenticated);

    if (isAuthenticated) {
      // Navigate to the authenticated screen
    }
  }
}
```

In the `BiometricAuthApp` widget, we create a simple login screen with an 'Authenticate with Biometrics' button. When the button is pressed, we authenticate the user using biometrics and save the authentication state using the `AuthStateManager`. If the authentication is successful, we can navigate the user to the authenticated screen.

## Conclusion

Implementing state restoration with biometric authentication adds an additional layer of security and provides a seamless user experience. With this implementation in Flutter, users can authenticate using their biometrics and have their authentication state restored when they revisit the app.

Remember to handle edge cases, such as when biometric data changes or is deleted, for a robust and secure implementation.