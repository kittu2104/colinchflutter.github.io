---
layout: post
title: "Using Firebase with MaterialApp for authentication."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In web and mobile app development, user authentication is a crucial aspect. Firebase, a mobile and web application development platform, offers a comprehensive authentication service that can be easily integrated into your application. In this tutorial, we will explore how to use Firebase authentication with MaterialApp, a popular UI framework for building Flutter applications.

## Table of Contents
- [Setting up Firebase](#setting-up-firebase)
- [Creating the MaterialApp](#creating-the-materialapp)
- [Implementing Firebase Authentication](#implementing-firebase-authentication)
- [Handling User Authentication](#handling-user-authentication)
- [Conclusion](#conclusion)

## Setting up Firebase

To get started, you need to have a Firebase project. If you haven't already, visit the [Firebase Console](https://console.firebase.google.com/) and create a new project. Once you have your project created, follow these steps to add Firebase to your Flutter project:

1. Add the `firebase_core` and `firebase_auth` packages to your `pubspec.yaml` file:

```yaml
dependencies:
  firebase_core: ^1.7.0
  firebase_auth: ^3.3.0
```

2. Run `flutter pub get` to fetch the packages.

3. Download the `google-services.json` file from the Firebase Console and place it in the `android/app` directory. For iOS, download the `GoogleService-Info.plist` file and add it to the `ios/Runner` directory.

## Creating the MaterialApp

Now that the Firebase setup is complete, let's create a MaterialApp in Flutter. The MaterialApp widget is used as the top-level widget in a Flutter app and provides several built-in features.

1. Create a new Flutter project using the following command:

```bash
flutter create my_app
```

2. Open the `lib/main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'My App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
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
        title: Text('Home'),
      ),
      body: Center(
        child: Text('Welcome to my app!'),
      ),
    );
  }
}
```

## Implementing Firebase Authentication

Let's now integrate Firebase authentication into our MaterialApp.

1. Create a new file `firebase_service.dart` and add the following code:

```dart
import 'package:firebase_auth/firebase_auth.dart';

class FirebaseService {
  final FirebaseAuth _auth = FirebaseAuth.instance;

  Future<String?> signInWithEmailAndPassword(String email, String password) async {
    try {
      final UserCredential userCredential = await _auth.signInWithEmailAndPassword(
        email: email,
        password: password,
      );
      return userCredential.user?.uid;
    } catch (e) {
      print(e.toString());
      return null;
    }
  }
}
```

2. In the `lib/main.dart` file, update the `MyHomePage` class with the following code to implement a basic login form:

```dart
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  final _formKey = GlobalKey<FormState>();
  final _emailController = TextEditingController();
  final _passwordController = TextEditingController();
  final _firebaseService = FirebaseService();

  String? _errorMessage;

  void _signIn() async {
    if (_formKey.currentState!.validate()) {
      final email = _emailController.text;
      final password = _passwordController.text;

      final userId = await _firebaseService.signInWithEmailAndPassword(email, password);

      if (userId != null) {
        // Navigate to home screen
      } else {
        setState(() {
          _errorMessage = 'Invalid credentials';
        });
      }
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Padding(
        padding: EdgeInsets.all(16.0),
        child: Form(
          key: _formKey,
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              if (_errorMessage != null)
                Text(
                  _errorMessage!,
                  style: TextStyle(color: Colors.red),
                ),
              TextFormField(
                controller: _emailController,
                decoration: InputDecoration(labelText: 'Email'),
                validator: (value) {
                  if (value!.isEmpty) {
                    return 'Please enter your email';
                  }
                  return null;
                },
              ),
              TextFormField(
                controller: _passwordController,
                obscureText: true,
                decoration: InputDecoration(labelText: 'Password'),
                validator: (value) {
                  if (value!.isEmpty) {
                    return 'Please enter your password';
                  }
                  return null;
                },
              ),
              SizedBox(height: 16.0),
              ElevatedButton(
                onPressed: _signIn,
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

## Handling User Authentication

With the above code, we have implemented a basic login form that uses Firebase authentication. When the user presses the "Sign In" button, the `_signIn` method is called. It validates the form inputs, calls the `signInWithEmailAndPassword` method of the `FirebaseService` class, and handles the result. If authentication is successful, you can navigate the user to the home screen of your app.

## Conclusion

In this tutorial, we learned how to use Firebase authentication with MaterialApp for user authentication in a Flutter app. Firebase provides a powerful and easy-to-use authentication service that can be seamlessly integrated into your application. By following the steps outlined in this tutorial, you can quickly implement user authentication in your Flutter app using Firebase. Happy coding!

_References:_
- [Flutter Documentation](https://flutter.dev/docs)
- [Firebase Authentication](https://firebase.google.com/products/auth)