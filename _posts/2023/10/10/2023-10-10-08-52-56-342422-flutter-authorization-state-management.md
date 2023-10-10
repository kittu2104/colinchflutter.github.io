---
layout: post
title: "Flutter authorization state management"
description: " "
date: 2023-10-10
tags: [Authorization]
comments: true
share: true
---

In any mobile app that requires user authentication and authorization, it is crucial to manage the authorization state properly. This ensures that users can securely access different features and data based on their permissions. In Flutter, there are several approaches to managing the authorization state, and in this blog post, we will explore some popular options.

## 1. Using Provider Package

Provider is a popular state management package for Flutter that enables efficient data sharing across your widget tree. Here's how you can use Provider to manage the authorization state:

1. Start by setting up the Provider package in your Flutter project by adding the following dependency to your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  provider: ^5.0.0
```

2. Create a class called `AuthState` that holds the current authorization state and any associated data. This class will extend `ChangeNotifier` from the Provider package.

```dart
import 'package:flutter/foundation.dart';

class AuthState extends ChangeNotifier {
  bool isAuthenticated = false;
  String userId = '';

  void login() {
    // Perform login logic
    isAuthenticated = true;
    userId = 'exampleUserId';

    notifyListeners();
  }

  void logout() {
    // Perform logout logic
    isAuthenticated = false;
    userId = '';

    notifyListeners();
  }
}
```

3. Wrap your root widget with a `ChangeNotifierProvider` widget and provide an instance of the `AuthState` class.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => AuthState(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Authorization State',
      home: HomePage(),
    );
  }
}
```

4. Access the `AuthState` instance in any widget using the `Provider.of<AuthState>(context)` method. For example, in a login page widget, you can call the `login()` and `logout()` methods, and update the UI accordingly.

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

class LoginPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final authState = Provider.of<AuthState>(context);

    return Scaffold(
      // ...
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            authState.login();
          },
          child: Text('Log In'),
        ),
      ),
    );
  }
}
```

## 2. BLoC Architecture

Another popular approach for managing the authorization state in Flutter is using the BLoC (Business Logic Component) architecture. BLoC separates business logic from the UI and provides a stream-based solution for managing state.

To implement authorization state management using BLoC:

1. Set up the `flutter_bloc` package in your Flutter project by adding the following dependency to your `pubspec.yaml` file:

```dart
dependencies:
  flutter:
    sdk: flutter
  flutter_bloc: ^7.0.0
```

2. Create a class called `AuthState` that represents the current authorization state and extends the `Equatable` class from the `equatable` package.

```dart
import 'package:equatable/equatable.dart';

class AuthState extends Equatable {
  final bool isAuthenticated;
  final String userId;

  AuthState({required this.isAuthenticated, required this.userId});

  @override
  List<Object> get props => [isAuthenticated, userId];
}
```

3. Create an `AuthEvent` class that defines the different events that can occur in the authentication flow, such as `LoginEvent` and `LogoutEvent`.

```dart
abstract class AuthEvent extends Equatable {
  @override
  List<Object> get props => [];
}

class LoginEvent extends AuthEvent {}
class LogoutEvent extends AuthEvent {}
```

4. Implement the `AuthBloc` class, which extends the `Bloc` class from the `flutter_bloc` package. This class receives `AuthEvent` objects and emits `AuthState` objects based on the logic implemented in its `mapEventToState` method.

```dart
import 'package:bloc/bloc.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

class AuthBloc extends Bloc<AuthEvent, AuthState> {
  AuthBloc() : super(AuthState(isAuthenticated: false, userId: ''));

  @override
  Stream<AuthState> mapEventToState(AuthEvent event) async* {
    if (event is LoginEvent) {
      // Perform login logic
      yield AuthState(isAuthenticated: true, userId: 'exampleUserId');
    } else if (event is LogoutEvent) {
      // Perform logout logic
      yield AuthState(isAuthenticated: false, userId: '');
    }
  }
}
```

5. Wrap your root widget with a `BlocProvider` widget and provide an instance of the `AuthBloc` class.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

void main() {
  runApp(
    BlocProvider(
      create: (context) => AuthBloc(),
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Authorization State',
      home: HomePage(),
    );
  }
}
```

6. Access the `AuthBloc` instance in any widget using the `BlocProvider.of<AuthBloc>(context)` method. For example, in a login page widget, you can dispatch a `LoginEvent` and `LogoutEvent` to trigger the appropriate state changes.

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

class LoginPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final authBloc = BlocProvider.of<AuthBloc>(context);

    return Scaffold(
      // ...
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            authBloc.add(LoginEvent());
          },
          child: Text('Log In'),
        ),
      ),
    );
  }
}
```

## Conclusion

Managing the authorization state is crucial for creating secure and user-friendly mobile apps. In this blog post, we explored two popular approaches, namely using the Provider package and implementing the BLoC architecture. Both options provide robust solutions, and the choice depends on the complexity and specific requirements of your app. Ensure to choose the approach that best fits your project's needs and enhances the user experience of your Flutter app.

**#Flutter** **#Authorization**