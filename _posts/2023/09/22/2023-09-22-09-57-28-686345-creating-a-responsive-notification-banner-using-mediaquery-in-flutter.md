---
layout: post
title: "Creating a responsive notification banner using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [flutter, notificationbanner]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive notification banner using the `MediaQuery` class in Flutter. This will allow us to display a notification banner at the top of the screen, and ensure that it adapts to different screen sizes.

## Prerequisites

Before we begin, make sure you have Flutter installed and set up on your machine. If not, [follow the installation instructions](https://flutter.dev/docs/get-started/install) on the Flutter website.

## Getting Started

1. Create a new Flutter project by running the following command in your terminal:
   ```
   flutter create notification_banner
   ```

2. Open the project in your preferred code editor.

3. Inside the `lib` directory, create a new file called `notification_banner.dart`.

4. In `notification_banner.dart`, add the following code to define a stateless widget:

   ```dart
   import 'package:flutter/material.dart';

   class NotificationBanner extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Container(
         height: MediaQuery.of(context).size.height * 0.1,
         color: Colors.blue, // Customize the color as per your requirement
         child: Center(
           child: Text(
             "New Notification!",
             style: TextStyle(
               color: Colors.white,
               fontSize: 18.0,
               fontWeight: FontWeight.bold,
             ),
           ),
         ),
       );
     }
   }
   ```

5. Now, open the `main.dart` file in the `lib` directory.

6. Delete the existing code inside the `main.dart` file and replace it with the following code:

   ```dart
   import 'package:flutter/material.dart';

   import 'notification_banner.dart';

   void main() {
     runApp(MyApp());
   }

   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return MaterialApp(
         title: 'Notification Banner Example',
         theme: ThemeData(
           primarySwatch: Colors.blue,
           visualDensity: VisualDensity.adaptivePlatformDensity,
         ),
         home: Scaffold(
           appBar: AppBar(
             title: Text('Notification Banner Example'),
           ),
           body: Column(
             children: [
               NotificationBanner(), // Add the notification banner here
               Expanded(
                 child: Center(
                   child: Text(
                     'Welcome to my app!',
                     style: TextStyle(fontSize: 24.0),
                   ),
                 ),
               ),
             ],
           ),
         ),
       );
     }
   }
   ```

## Testing the Notification Banner

Save all the changes and run the app by executing the following command in your terminal:

```
flutter run
```

The app will launch in the simulator or on your connected device.

You will now see a notification banner at the top of the screen, with the message "New Notification!" centered within it. The banner will adapt its height based on the screen size using `MediaQuery.of(context).size.height * 0.1`.

Congratulations! You have successfully created a responsive notification banner using `MediaQuery` in Flutter.

#flutter #notificationbanner