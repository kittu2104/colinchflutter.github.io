---
layout: post
title: "Implementing responsive form validation using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [ResponsiveDesign]
comments: true
share: true
---

In Flutter, `MediaQuery` is a powerful class that allows us to access various properties of the device, such as its size, orientation, and pixel density. By leveraging `MediaQuery`, we can implement responsive form validation to ensure that our forms adapt to different screen sizes and orientations.

## 1. Setting up the project

To get started, create a new Flutter project and navigate to the main Dart file. Import the necessary packages:

```dart
import 'package:flutter/material.dart';
```

## 2. Creating the form

Next, create a class to represent the form. In this example, we'll create a simple registration form with fields for name, email, and password. The `Form` widget provides built-in form validation capabilities:

```dart
class RegistrationForm extends StatelessWidget {
  final _formKey = GlobalKey<FormState>();
  
  @override
  Widget build(BuildContext context) {
    return Form(
      key: _formKey,
      child: Column(
        children: [
          TextFormField(
            decoration: InputDecoration(labelText: 'Name'),
            validator: (value) {
              if (value.isEmpty) {
                return 'Please enter your name.';
              }
              return null;
            },
          ),
          TextFormField(
            decoration: InputDecoration(labelText: 'Email'),
            validator: (value) {
              if (value.isEmpty || !value.contains('@')) {
                return 'Please enter a valid email address.';
              }
              return null;
            },
          ),
          TextFormField(
            decoration: InputDecoration(labelText: 'Password'),
            obscureText: true,
            validator: (value) {
              if (value.length < 6) {
                return 'Password must be at least 6 characters long.';
              }
              return null;
            },
          ),
          RaisedButton(
            onPressed: () {
              if (_formKey.currentState.validate()) {
                // Form is valid, proceed with registration
              }
            },
            child: Text('Register'),
          ),
        ],
      ),
    );
  }
}
```

## 3. Implementing responsive validation

Now we can modify the `RegistrationForm` class to make it responsive using `MediaQuery`. Let's say we want to display a different TextFormField appearance and validation error message for large screens. We can achieve this by checking the device's screen width:

```dart
class RegistrationForm extends StatelessWidget {
  final _formKey = GlobalKey<FormState>();
  
  @override
  Widget build(BuildContext context) {
    final screenWidth = MediaQuery.of(context).size.width;
    final isLargeScreen = screenWidth > 600;
    
    return Form(
      key: _formKey,
      child: Column(
        children: [
          TextFormField(
            decoration: InputDecoration(
              labelText: 'Name',
              fontStyle: isLargeScreen ? FontStyle.normal : FontStyle.italic,
            ),
            validator: (value) {
              if (value.isEmpty) {
                return isLargeScreen ? 'Please enter your name.' : 'Name is required.';
              }
              return null;
            },
          ),
          TextFormField(
            decoration: InputDecoration(
              labelText: 'Email',
              fillColor: isLargeScreen ? Colors.blueAccent : Colors.white,
            ),
            validator: (value) {
              if (value.isEmpty || !value.contains('@')) {
                return isLargeScreen ? 'Please enter a valid email address.' : 'Invalid email.';
              }
              return null;
            },
          ),
          TextFormField(
            decoration: InputDecoration(labelText: 'Password'),
            obscureText: true,
            validator: (value) {
              if (value.length < 6) {
                return 'Password must be at least 6 characters long.';
              }
              return null;
            },
          ),
          RaisedButton(
            onPressed: () {
              if (_formKey.currentState.validate()) {
                // Form is valid, proceed with registration
              }
            },
            child: Text('Register'),
          ),
        ],
      ),
    );
  }
}
```

## Conclusion

By using `MediaQuery` in Flutter, we can easily implement responsive form validation. We demonstrated how to adapt form fields' appearances and error messages based on the screen size. This ensures an optimal user experience across different devices and orientations. Make your forms more resilient to varying screen sizes and provide meaningful feedback to users with responsive form validation in Flutter.

#Flutter #ResponsiveDesign