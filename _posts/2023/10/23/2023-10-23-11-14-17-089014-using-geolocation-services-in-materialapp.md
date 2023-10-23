---
layout: post
title: "Using geolocation services in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In today's increasingly connected world, geolocation services have become an integral part of many mobile and web applications. These services allow developers to obtain the current physical location of a device, enabling them to offer personalized and location-based experiences to users.

If you are building a mobile application using the Flutter framework, specifically using the `MaterialApp` widget, you can easily incorporate geolocation services into your app. Here's how you can do it:

## Step 1: Add dependencies

To access geolocation services in your Flutter app, you'll need to include the `geolocator` package. Open your `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  geolocator: ^7.0.0
```

Save the file, and run the command `flutter pub get` in your terminal or IDE to download the package.

## Step 2: Request location permissions

Before you can access the user's location, you need to request permission from the user. You can use the `permission_handler` package to handle this. Add the following code snippet to your app's entry point (usually in the `main.dart` file) to request location permissions:

```dart
import 'package:permission_handler/permission_handler.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Permission.location.request();
  runApp(MyApp());
}
```

## Step 3: Access the user's location

Once you have obtained the necessary permissions, you can start accessing the user's location. To do this, you need to use the `geolocator` package.

First, import the package in your `dart` file:

```dart
import 'package:geolocator/geolocator.dart';
```

Next, define a function that fetches the user's current location:

```dart
Future<Position> getLocation() async {
  bool serviceEnabled;
  LocationPermission permission;

  // Check if location services are enabled
  serviceEnabled = await Geolocator.isLocationServiceEnabled();

  // If services are not enabled, prompt the user to enable them
  if (!serviceEnabled) {
    return Future.error('Location services are disabled.');
  }

  // Request location permissions if not already granted
  permission = await Geolocator.checkPermission();
  if (permission == LocationPermission.denied) {
    permission = await Geolocator.requestPermission();
    if (permission == LocationPermission.deniedForever) {
      return Future.error(
          'Location permissions are permanently denied, we cannot request permissions.');
    }

    if (permission == LocationPermission.denied) {
      return Future.error('Location permissions are denied');
    }
  }

  // Get the current location
  return await Geolocator.getCurrentPosition();
}
```

Finally, you can call this function to obtain the user's location. For example, you can display it in your `MaterialApp` as follows:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Geolocation App'),
        ),
        body: Center(
          child: ElevatedButton(
            onPressed: () async {
              // Fetch the user's location
              Position position = await getLocation();
              // Display the latitude and longitude
              ScaffoldMessenger.of(context).showSnackBar(
                SnackBar(
                  content: Text(
                    'Latitude: ${position.latitude}, Longitude: ${position.longitude}',
                  ),
                ),
              );
            },
            child: Text('Get Location'),
          ),
        ),
      ),
    );
  }
}
```

That's it! You have now integrated geolocation services into your `MaterialApp` Flutter app. Whenever the user taps the "Get Location" button, the app will request their location and display it using a snackbar.

Remember to handle cases where the user denies permission or disables location services, providing appropriate error messages or fallback behavior.

Using geolocation services can greatly enhance your app's functionality, allowing you to deliver personalized experiences based on the user's physical location. Start exploring the possibilities today!

For more details on the `geolocator` package, refer to the official [documentation](https://pub.dev/packages/geolocator).