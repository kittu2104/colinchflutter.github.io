---
layout: post
title: "Implementing state restoration with deep linking in Flutter"
description: " "
date: 2023-09-15
tags: [Flutter, StateRestoration, DeepLinking]
comments: true
share: true
---

Flutter is a popular cross-platform framework for building beautiful and performant mobile applications. One important feature that Flutter offers is the ability to implement state restoration with deep linking. This functionality allows your app to remember its state and restore it when the app is relaunched or deep linked from another app or website. In this blog post, we will explore how to implement state restoration with deep linking in Flutter.

## What is State Restoration?

State restoration is the ability of an app to remember and restore its state when it is terminated and relaunched. This is particularly useful in mobile apps where users often switch between different apps or navigate away from an app and then return to it.

## Deep Linking

Deep linking is a mechanism that allows users to navigate directly to a specific screen or content within an app from another app or website. It is a powerful feature that improves user experience and engagement.

## Implementing State Restoration

To implement state restoration in your Flutter app, follow these steps:

1. Add the `flutter_bloc` package to your `pubspec.yaml` file.

   ```yaml
   dependencies:
     flutter:
       sdk: flutter
     flutter_bloc: ^7.0.0
   ```

2. Create a `AppState` class to store the necessary state of your app. This class should extend `Equatable` from the `equatable` package.

   ```dart
   import 'package:equatable/equatable.dart';

   class AppState extends Equatable {
     final int counter;

     AppState(this.counter);

     @override
     List<Object> get props => [counter];
   }
   ```

3. Create a `AppBloc` class to manage the app state using the `flutter_bloc` package. This class should extend `Bloc` from the `flutter_bloc` package.

   ```dart
   import 'package:bloc/bloc.dart';

   class AppBloc extends Bloc<dynamic, AppState> {
     AppBloc() : super(AppState(0));

     @override
     Stream<AppState> mapEventToState(dynamic event) async* {
       // Add logic to handle events and update the app state
     }
   }
   ```

4. Wrap your app's root widget with the `BlocProvider` widget from the `flutter_bloc` package. This will provide the `AppBloc` instance to all descendant widgets.

   ```dart
   import 'package:flutter/material.dart';
   import 'package:flutter_bloc/flutter_bloc.dart';

   void main() {
     runApp(BlocProvider(
       create: (context) => AppBloc(),
       child: MyApp(),
     ));
   }

   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return MaterialApp(
         title: 'State Restoration with Deep Linking',
         theme: ThemeData(
           primarySwatch: Colors.blue,
         ),
         home: MyHomePage(),
       );
     }
   }
   ```

5. Implement deep linking by handling the deep link URL in your app's entry point. Use the `getInitialRoute` method from the `WidgetsFlutterBinding` class to get the initial route based on the deep link.

   ```dart
   import 'package:flutter/material.dart';
   import 'package:flutter/services.dart';
   import 'package:flutter_bloc/flutter_bloc.dart';

   void main() {
     WidgetsFlutterBinding.ensureInitialized();

     // Handle deep link URL
     handleDeepLink();

     runApp(BlocProvider(
       create: (context) => AppBloc(),
       child: MyApp(),
     ));
   }

   Future<void> handleDeepLink() async {
     // Get initial route based on deep link URL
     final String initialRoute = await getInitialRoute();

     // Navigate to the specified route
     runApp(BlocProvider(
       create: (context) => AppBloc(),
       child: MaterialApp(
         title: 'State Restoration with Deep Linking',
         initialRoute: initialRoute,
         theme: ThemeData(
           primarySwatch: Colors.blue,
         ),
         home: MyHomePage(),
       ),
     ));
   }

   Future<String> getInitialRoute() async {
     // Replace with your own logic to retrieve the deep link URL
     final String deepLinkUrl = await getDeepLinkUrl();

     // Replace with your own logic to parse the deep link URL and get the initial route
     return parseDeepLink(deepLinkUrl);
   }
   ```

6. Update the app state based on the deep link data in your `AppBloc` class. This can be done by listening to events using the `mapEventToState` method.

   ```dart
   import 'package:bloc/bloc.dart';

   class AppBloc extends Bloc<dynamic, AppState> {
     AppBloc() : super(AppState(0));

     @override
     Stream<AppState> mapEventToState(dynamic event) async* {
       if (event is DeepLinkEvent) {
         // Update app state based on the deep link data
         yield AppState(event.counter);
       }
     }
   }

   class DeepLinkEvent {
     final int counter;

     DeepLinkEvent(this.counter);
   }
   ```

7. Finally, update your UI widgets to reflect the app state. This can be done by wrapping relevant widgets with the `BlocBuilder` widget from the `flutter_bloc` package.

   ```dart
   import 'package:flutter/material.dart';
   import 'package:flutter_bloc/flutter_bloc.dart';

   class MyHomePage extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: Text('State Restoration with Deep Linking'),
         ),
         body: Center(
           child: BlocBuilder<AppBloc, AppState>(
             builder: (context, state) {
               return Text(
                 'Counter: ${state.counter}',
                 style: TextStyle(fontSize: 24),
               );
             },
           ),
         ),
       );
     }
   }
   ```

## Conclusion

State restoration with deep linking is a powerful feature that can greatly improve the user experience of your Flutter app. By following the steps outlined in this blog post, you can easily implement state restoration with deep linking in your Flutter app and ensure that users can seamlessly navigate and return to their previous app state.

#Flutter #StateRestoration #DeepLinking