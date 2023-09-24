---
layout: post
title: "Implementing social media authentication in a StatelessWidget in Flutter"
description: " "
date: 2023-09-24
tags: []
comments: true
share: true
---

In today's digital world, social media authentication has become an essential part of many applications. It provides users with a convenient way to sign in to apps using their existing social media accounts, eliminating the need to create a new username and password. In this blog post, we will explore how to implement social media authentication in a `StatelessWidget` in Flutter.

## Prerequisites
Before we begin, make sure you have the following requirements:

- Flutter SDK installed on your machine
- A basic understanding of Flutter and Dart programming language

## Step 1: Setting up Dependencies
To authenticate users using social media accounts, we first need to add the necessary dependencies to our `pubspec.yaml` file. Open the file and add the following dependencies:

```yaml
dependencies:
  flutter_facebook_login: ^3.0.0
  google_sign_in: ^5.0.0
```

Save the file and run the following command in your terminal to fetch the dependencies:

```bash
flutter pub get
```

## Step 2: Configuring Social Media Platforms
Before we can implement authentication, we need to configure our social media platforms through their respective developer portals. For this example, let's consider Facebook and Google authentication.

### Facebook Authentication
1. Go to the [Facebook Developer Portal](https://developers.facebook.com/) and create a new app.
2. Retrieve your `App ID` and add it to your Flutter project by adding the following code to your `android/app/src/main/AndroidManifest.xml` file:

```xml
<meta-data
    android:name="com.facebook.sdk.ApplicationId"
    android:value="@string/facebook_app_id" />
```
    
3. Replace the `@string/facebook_app_id` value with your actual `App ID`.

### Google Authentication
1. Go to the [Google Cloud Console](https://console.cloud.google.com/) and create a new project.
2. Enable the `Google Sign-in API` for the created project.
3. Generate an `OAuth 2.0 Client ID` and save its `Client ID` value.

## Step 3: Implementing Authentication in StatelessWidget
Now that we have our dependencies and social media platforms configured, let's implement the authentication in our `StatelessWidget`. 

First, import the necessary packages at the top of your file:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_facebook_login/flutter_facebook_login.dart';
import 'package:google_sign_in/google_sign_in.dart';
```

Next, define the methods for Facebook and Google authentication:

```dart
final facebookLogin = FacebookLogin();
final googleSignIn = GoogleSignIn(scopes: ['email']);

Future<void> loginWithFacebook() async {
  final result = await facebookLogin.logIn(['email']);

  switch (result.status) {
    case FacebookLoginStatus.loggedIn:
      // User successfully authenticated. Proceed with your logic.
      break;

    case FacebookLoginStatus.cancelledByUser:
      // User cancelled the authentication process.
      break;

    case FacebookLoginStatus.error:
      // An error occurred during authentication.
      break;
  }
}

Future<void> loginWithGoogle() async {
  try {
    final account = await googleSignIn.signIn();
    // User successfully authenticated. Proceed with your logic.
  } catch (error) {
    // An error occurred during authentication.
  }
}
```

Finally, add the authentication methods to your `StatelessWidget`'s build method:

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text("Social Media Auth"),
    ),
    body: Center(
      child: Column(
        mainAxisAlignment: MainAxisAlignment.center,
        children: [
          RaisedButton(
            onPressed: loginWithFacebook,
            child: Text("Login with Facebook"),
          ),
          RaisedButton(
            onPressed: loginWithGoogle,
            child: Text("Login with Google"),
          ),
        ],
      ),
    ),
  );
}
```

Make sure to provide appropriate callbacks and error handling logic inside the authentication methods.

## Conclusion
Implementing social media authentication in a `StatelessWidget` in Flutter is a straightforward process. By following the steps outlined in this blog post, you can empower your app users to authenticate using their social media accounts.