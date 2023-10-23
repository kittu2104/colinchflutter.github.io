---
layout: post
title: "Building restaurant reservation and order apps with MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In this blog post, we will explore how to build restaurant reservation and order apps using the MaterialApp package in Flutter. The MaterialApp package provides a set of pre-designed widgets and themes that can be easily customized to create beautiful and functional user interfaces.

## Table of Contents

- [Introduction](#introduction)
- [Setting up the project](#setting-up-the-project)
- [Implementing the reservation feature](#implementing-the-reservation-feature)
- [Implementing the order feature](#implementing-the-order-feature)
- [Conclusion](#conclusion)

## Introduction

In the world of mobile apps, restaurant reservation and order apps have become increasingly popular. These apps allow users to conveniently book a table at their favorite restaurant and also place an order for pickup or delivery. With the help of the MaterialApp package, we can quickly create an intuitive and visually appealing interface for these apps.

## Setting up the project

To create a Flutter project with MaterialApp, first, make sure you have Flutter and Dart installed on your machine. Then, open your favorite IDE and follow these steps:

1. Create a new Flutter project:
   ```dart
   flutter create restaurant_app
   ```

2. Open the project in your IDE:
   ```dart
   cd restaurant_app
   ```

3. Update the `pubspec.yaml` file to include the MaterialApp package:
   ```yaml
   dependencies:
     flutter:
       sdk: flutter
     cupertino_icons: ^1.0.2
     material_app: ^1.0.0
   ```

4. Run `flutter pub get` to fetch the dependencies:
   ```dart
   flutter pub get
   ```

5. Replace the contents of the `lib/main.dart` file with the following code:
   ```dart
   import 'package:flutter/material.dart';

   void main() {
     runApp(MyApp());
   }

   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return MaterialApp(
         title: 'Restaurant App',
         theme: ThemeData(
           primarySwatch: Colors.blue,
           visualDensity: VisualDensity.adaptivePlatformDensity,
         ),
         home: RestaurantAppHome(),
       );
     }
   }

   class RestaurantAppHome extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: Text('Restaurant App'),
         ),
         body: Center(
           child: Text('Welcome to the Restaurant App!'),
         ),
       );
     }
   }
   ```

6. Save the file and run the app:
   ```dart
   flutter run
   ```

You should now have a basic Flutter app with MaterialApp set up.

## Implementing the reservation feature

To implement the reservation feature, we can create a new screen where users can select the desired date and time for their reservation. We can use date and time picker widgets provided by MaterialApp to make the selection process easier for users.

Here's an example of how the reservation screen might look:

```dart
class ReservationScreen extends StatefulWidget {
  @override
  _ReservationScreenState createState() => _ReservationScreenState();
}

class _ReservationScreenState extends State<ReservationScreen> {
  DateTime selectedDate;
  TimeOfDay selectedTime;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Make a Reservation'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            RaisedButton(
              child: Text('Select Date'),
              onPressed: () async {
                final DateTime picked = await showDatePicker(
                  context: context,
                  initialDate: DateTime.now(),
                  firstDate: DateTime.now(),
                  lastDate: DateTime(DateTime.now().year + 1),
                );
                if (picked != null && picked != selectedDate) {
                  setState(() {
                    selectedDate = picked;
                  });
                }
              },
            ),
            SizedBox(height: 20),
            RaisedButton(
              child: Text('Select Time'),
              onPressed: () async {
                final TimeOfDay picked =
                    await showTimePicker(context: context, initialTime: TimeOfDay.now());
                if (picked != null && picked != selectedTime) {
                  setState(() {
                    selectedTime = picked;
                  });
                }
              },
            ),
            SizedBox(height: 20),
            Text(
              'Selected Date: ${selectedDate?.toString() ?? "Not Selected"}',
            ),
            SizedBox(height: 10),
            Text(
              'Selected Time: ${selectedTime?.format(context) ?? "Not Selected"}',
            ),
          ],
        ),
      ),
    );
  }
}
```

## Implementing the order feature

Similarly, we can create a screen for placing orders where users can select the items they want to order and specify any additional preferences. We can use various widgets provided by MaterialApp, such as ListView, CheckboxListTile, TextFormField, etc., to create an interactive and user-friendly order screen.

Here's an example of how the order screen might look:

```dart
class OrderScreen extends StatefulWidget {
  @override
  _OrderScreenState createState() => _OrderScreenState();
}

class _OrderScreenState extends State<OrderScreen> {
  List<String> selectedItems = [];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Place an Order'),
      ),
      body: ListView(
        children: [
          CheckboxListTile(
            title: Text('Item 1'),
            value: selectedItems.contains('Item 1'),
            onChanged: (value) {
              setState(() {
                if (value) {
                  selectedItems.add('Item 1');
                } else {
                  selectedItems.remove('Item 1');
                }
              });
            },
          ),
          CheckboxListTile(
            title: Text('Item 2'),
            value: selectedItems.contains('Item 2'),
            onChanged: (value) {
              setState(() {
                if (value) {
                  selectedItems.add('Item 2');
                } else {
                  selectedItems.remove('Item 2');
                }
              });
            },
          ),
          SizedBox(height: 20),
          TextFormField(
            decoration: InputDecoration(
              labelText: 'Additional Preferences',
              hintText: 'e.g. No onions',
            ),
            maxLines: null,
          ),
          SizedBox(height: 20),
          RaisedButton(
            child: Text('Place Order'),
            onPressed: () {
              // Implement order placement logic here
            },
          ),
        ],
      ),
    );
  }
}
```

## Conclusion

By leveraging the MaterialApp package, building restaurant reservation and order apps in Flutter becomes a much simpler task. The package provides a range of pre-designed widgets and themes that can be customized to match the desired design aesthetic. Whether it's implementing a reservation feature or an order placement feature, MaterialApp offers a set of powerful widgets that make the development process efficient and enjoyable.

Happy coding! 🚀

# References

- [MaterialApp API documentation](https://api.flutter.dev/flutter/material/MaterialApp-class.html)
- [Flutter documentation](https://flutter.dev/docs)