---
layout: post
title: "Integrating Flutter Alarm Manager with Google Calendar API"
description: " "
date: 2023-09-18
tags: [GoogleCalendarAPI]
comments: true
share: true
---

In today's fast-paced world, staying organized and managing our time efficiently is crucial. Flutter, a popular cross-platform framework, allows developers to create beautiful and interactive mobile applications. In this article, we will explore how to integrate Flutter Alarm Manager with the Google Calendar API, enabling users to schedule alarms based on events from their Google Calendar.

## Prerequisites

- Flutter installed on your development machine
- An active Google account
- Basic knowledge of using APIs and making HTTP requests

## Steps to integrate Flutter Alarm Manager with Google Calendar API

### Step 1: Create a new Flutter project

First, let's create a new Flutter project by running the following command in your terminal:

```bash
flutter create flutter_alarm_manager
```

### Step 2: Set up authentication with Google Calendar API

To access the Google Calendar API, we need to obtain OAuth 2.0 credentials. Here's how you can set up authentication:

1. Go to the [Google Cloud Console](https://console.cloud.google.com/).
2. Create a new project or select an existing one.
3. Enable the **Google Calendar API** for your project.
4. Go to the **Credentials** page and click on **Create Credentials**.
5. Select **OAuth client ID** as the credential type.
6. Choose **Android** as the application type.
7. Provide a name for your OAuth client ID and enter your **Package name**.
8. Paste the **SHA-1 fingerprint** of your debug keystore certificate. You can generate it by running the following command in your terminal:

   ```bash
   keytool -list -v -alias androiddebugkey -keystore $HOME/.android/debug.keystore
   ```

9. Save the generated credentials, which will be used later in our Flutter application.

### Step 3: Add necessary dependencies

Open the `pubspec.yaml` file in your Flutter project and add the following dependencies:

```yaml
dependencies:
  flutter:
    sdk: flutter
  http: ^0.13.4
  google_sign_in: ^5.1.0
  flutter_secure_storage: ^5.0.2
  flutter_alarm_manager: ^1.0.0
```

Run `flutter pub get` in your terminal to fetch the new dependencies.

### Step 4: Implement authentication with Google Sign-In

In your Flutter application, import the necessary packages:

```dart
import 'package:http/http.dart' as http;
import 'package:flutter_secure_storage/flutter_secure_storage.dart';
import 'package:google_sign_in/google_sign_in.dart';
```

Next, create a singleton class to handle authentication with Google Sign-In:

```dart
class GoogleAuth {
  static final GoogleAuth _instance = GoogleAuth._internal();

  final GoogleSignIn _googleSignIn = GoogleSignIn(
    scopes: ['email', 'https://www.googleapis.com/auth/calendar.readonly'],
  );

  final http.Client _httpClient = http.Client();
  final FlutterSecureStorage _secureStorage = FlutterSecureStorage();

  factory GoogleAuth() {
    return _instance;
  }

  GoogleAuth._internal();

  Future<void> signIn() async {
    try {
      final GoogleSignInAccount? googleUser = await _googleSignIn.signIn();
      final GoogleSignInAuthentication googleAuth = await googleUser!.authentication;

      // Store the access token securely for future API requests
      await _secureStorage.write(key: 'accessToken', value: googleAuth.accessToken);
    } catch (e) {
      print('Failed to sign in with Google: $e');
    }
  }

  Future<void> signOut() async {
    await _googleSignIn.signOut();
    await _secureStorage.delete(key: 'accessToken');
  }

  Future<String?> getAccessToken() async {
    return await _secureStorage.read(key: 'accessToken');
  }
}
```

The `signIn()` method initiates the Google Sign-In flow and stores the access token securely using `flutter_secure_storage`. The `signOut()` method handles signing out the user, and `getAccessToken()` retrieves the stored access token.

### Step 5: Fetch events from Google Calendar API

Next, let's retrieve events from the user's Google Calendar. Add the following code to your Flutter application:

```dart
class CalendarEvent {
  final String summary;
  final DateTime startDate;

  CalendarEvent(this.summary, this.startDate);
}

class CalendarService {
  final GoogleAuth _googleAuth = GoogleAuth();
  final http.Client _httpClient = http.Client();

  Future<List<CalendarEvent>> fetchEvents() async {
    final accessToken = await _googleAuth.getAccessToken();

    if (accessToken == null) {
      print('Access token not found');
      return [];
    }

    final response = await _httpClient.get(
      Uri.parse('https://www.googleapis.com/calendar/v3/calendars/primary/events'),
      headers: {
        'Authorization': 'Bearer $accessToken',
      },
    );

    if (response.statusCode == 200) {
      final List<dynamic> jsonEvents = jsonDecode(response.body)['items'];

      final List<CalendarEvent> events = jsonEvents.map((json) {
        final String summary = json['summary'];
        final DateTime startDate = DateTime.parse(json['start']['dateTime']);

        return CalendarEvent(summary, startDate);
      }).toList();

      return events;
    } else {
      print('Failed to fetch events: ${response.statusCode}');
      return [];
    }
  }
}
```

The `fetchEvents()` method retrieves events from the user's primary calendar using the access token retrieved from `GoogleAuth`. It parses the JSON response and converts each event into a `CalendarEvent` object.

### Step 6: Schedule alarms with Flutter Alarm Manager

Lastly, let's use the Flutter Alarm Manager plugin to schedule alarms based on the fetched events. Add the following code to your Flutter application:

```dart
import 'package:flutter_alarm_manager/flutter_alarm_manager.dart';

class AlarmScheduler {
  final CalendarService _calendarService = CalendarService();

  Future<void> scheduleAlarms() async {
    final List<CalendarEvent> events = await _calendarService.fetchEvents();

    // Cancel all existing alarms
    FlutterAlarmManager.cancelAll();

    for (final event in events) {
      // Schedule an alarm based on the event's start date
      FlutterAlarmManager.schedule(
        alarmDateTime: event.startDate.subtract(const Duration(minutes: 15)),
        alarmTitle: 'Event Reminder',
        alarmMessage: 'You have an event: ${event.summary}',
      );
    }
  }
}
```

The `scheduleAlarms()` method fetches events using `CalendarService` and schedules an alarm for each event. We subtract 15 minutes from the event's start date to give the user a reminder before the event.

## Conclusion

In this article, we learned how to integrate Flutter Alarm Manager with the Google Calendar API. By combining these two powerful tools, you can create a highly efficient and organized scheduling system in your Flutter applications. Remember to handle exceptions and provide appropriate error handling for a more robust user experience. Happy coding!

#Flutter  #GoogleCalendarAPI