---
layout: post
title: "Building ticket booking and event management features with MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In this tech blog post, we will explore how to build ticket booking and event management features using the `MaterialApp` widget in Flutter. 

## Table of Contents
- [Introduction](#introduction)
- [Setting up the project](#setting-up-the-project)
- [Creating the ticket booking page](#creating-the-ticket-booking-page)
- [Implementing event management](#implementing-event-management)
- [Conclusion](#conclusion)

## Introduction

Ticket booking and event management are essential components of many applications. With Flutter and the `MaterialApp` widget, we can easily create a seamless and interactive user experience for booking tickets and managing events.

## Setting up the project

Before we begin, make sure you have Flutter installed on your system. You can check this by running `flutter doctor` in your terminal.

To create a new Flutter project, run the following command:

```bash
flutter create ticket_booking_app
```

Once the project is created, navigate to the project directory using `cd ticket_booking_app`.

## Creating the ticket booking page

Now, let's create a ticket booking page where users can select the event, number of tickets, and proceed towards booking. We will use the `MaterialApp` widget to manage the overall structure and look of the app.

Start by opening the `lib/main.dart` file and replace the default code with the following:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Ticket Booking App',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TicketBookingPage(),
    );
  }
}

class TicketBookingPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // TODO: Implement ticket booking UI
    return Scaffold(
      appBar: AppBar(
        title: Text('Ticket Booking'),
      ),
      body: Center(
        child: Text('Ticket Booking Page'),
      ),
    );
  }
}
```

In the above code, we create a `MyApp` widget which extends `StatelessWidget` and sets up the `MaterialApp` with a title and theme. Inside the `MaterialApp`, we set the `home` property to `TicketBookingPage`, which is a new class we define for the ticket booking UI.

The `TicketBookingPage` is a `StatelessWidget` that returns a `Scaffold` widget. We have added an `AppBar` with a title and a placeholder text in the `body`.

## Implementing event management

Now that we have the basic ticket booking page set up, let's move on to implementing event management. We can create a separate screen to display the available events and enable users to add new events.

To add event management, start by creating a new file called `event_management.dart` in the `lib` directory. Add the following code to it:

```dart
import 'package:flutter/material.dart';

class EventManagementPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Event Management'),
      ),
      body: Center(
        child: Text('Event Management Page'),
      ),
    );
  }
}
```

Next, open the `lib/main.dart` file and update the `TicketBookingPage` class to include an event management button. Modify the code as follows:

```dart
class TicketBookingPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Ticket Booking'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Ticket Booking Page'),
            RaisedButton(
              onPressed: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(
                    builder: (context) => EventManagementPage(),
                  ),
                );
              },
              child: Text('Manage Events'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In the updated code, we added a `RaisedButton` widget within the `Column` widget. When the button is pressed, it navigates to the `EventManagementPage`. We achieve this using the `Navigator.push` method and specifying the `EventManagementPage` as the target.

## Conclusion

In this blog post, we explored how to build ticket booking and event management features using the Flutter `MaterialApp` widget. We started by setting up the project and creating the ticket booking page. Then, we implemented event management by adding a separate page and a button to navigate to it. With Flutter and `MaterialApp`, building interactive and visually appealing ticket booking and event management features is straightforward.

Stay tuned for more Flutter tutorials and happy coding!

# References

- [Flutter documentation](https://flutter.dev/docs)
- [MaterialApp class documentation](https://api.flutter.dev/flutter/material/MaterialApp-class.html)