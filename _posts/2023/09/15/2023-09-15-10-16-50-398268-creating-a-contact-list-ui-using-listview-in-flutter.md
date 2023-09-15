---
layout: post
title: "Creating a contact list UI using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [flutter, flutterdev]
comments: true
share: true
---

In this blog post, we will explore how to create a contact list user interface (UI) using `ListView` in Flutter. This UI will allow users to view a list of contacts and interact with them seamlessly.

## Prerequisites

Before we start, make sure you have Flutter and Dart installed on your machine. If not, please follow the official Flutter installation guide to set up the necessary tools.

## Steps

### Step 1: Set up a new Flutter project

Open your preferred IDE (Integrated Development Environment) and create a new Flutter project. Name the project "ContactListUI".

### Step 2: Add necessary dependencies

Navigate to the `pubspec.yaml` file in your Flutter project and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter

  # Add dependencies for contact list UI
  # Example:
  # contact_service: ^0.6.2
```

Uncomment and modify the `contact_service` dependency as per your requirements. This dependency allows us to fetch contact data.

### Step 3: Create a Contact model

Create a new Dart file `contact.dart` and define a `Contact` class to represent a single contact. Add the necessary properties such as name, phone number, and email.

```dart
class Contact {
  String name;
  String phoneNumber;
  String email;

  Contact({
    required this.name,
    required this.phoneNumber,
    required this.email,
  });
}
```

### Step 4: Fetch contact data

Inside the main application widget, fetch contact data using the `contact_service` dependency. Store the contacts in a list.

```dart
import 'package:contact_service/contact_service.dart';

Future<List<Contact>> fetchContacts() async {
  // Fetch contacts using contact_service package
  // Example:
  // final contacts = await ContactsService.getContacts();
  // Transform the fetched contacts into our Contact model

  return [];
}
```

### Step 5: Create the contact list UI

Replace the default `Container` with a `ListView.builder` widget inside the `build` method of the main application widget.

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: Text('Contact List'),
    ),
    body: FutureBuilder<List<Contact>>(
      future: fetchContacts(),
      builder: (context, snapshot) {
        if (snapshot.hasData) {
          final contacts = snapshot.data;

          return ListView.builder(
            itemCount: contacts.length,
            itemBuilder: (context, index) {
              final contact = contacts[index];

              return ListTile(
                title: Text(contact.name),
                subtitle: Text(contact.phoneNumber),
                trailing: Icon(Icons.arrow_forward),
                // Add more UI components or functionality as needed
              );
            },
          );
        } else if (snapshot.hasError) {
          return Text('Error fetching contacts');
        } else {
          return Center(
            child: CircularProgressIndicator(),
          );
        }
      },
    ),
  );
}
```

### Step 6: Run the app

Save the changes and run the app using the `flutter run` command in the terminal. You should now see a contact list UI populated with contact data.

## Conclusion

By following these steps, you have successfully created a contact list user interface using `ListView` in Flutter. This UI can be further customized and extended to meet the specific requirements of your app. Happy coding!

#flutter #flutterdev