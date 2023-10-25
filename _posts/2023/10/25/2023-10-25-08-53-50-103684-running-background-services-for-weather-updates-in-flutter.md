---
layout: post
title: "Running background services for weather updates in Flutter"
description: " "
date: 2023-10-25
tags: []
comments: true
share: true
---

In mobile app development, it is often necessary to run background services to fetch data periodically, such as weather updates. In Flutter, we can achieve this by using a combination of native platform code and Flutter plugins.

## Setup

1. Create a new Flutter project using the Flutter CLI or your preferred IDE.
2. Open the project in your IDE and navigate to the `android` folder.
3. Open the `app > src > main > java` folder and create a new package called `background`.
4. Inside the `background` package, create a new Java class file, `WeatherUpdateService.java`.

## Implementing the background service

Inside the `WeatherUpdateService.java` file, we need to extend the `IntentService` class and override the `onHandleIntent` method. This method will be called every time our service is started.

```java
package com.example.weatherapp.background;
import android.app.IntentService;
import android.content.Intent;
import androidx.annotation.Nullable;

public class WeatherUpdateService extends IntentService {

    public WeatherUpdateService() {
        super("WeatherUpdateService");
    }

    @Override
    protected void onHandleIntent(@Nullable Intent intent) {
        // Perform your weather update logic here
    }
}
```

## Registering the service

To use the service in our Flutter app, we need to register it in the AndroidManifest.xml file. Open the `android > app > src > main > AndroidManifest.xml` file and add the following lines inside the `<application>` tag.

```xml
<service
    android:name=".background.WeatherUpdateService"
    android:exported="false" />
```

## Invoking the service from Flutter

To start the background service from Flutter, we can use a Flutter plugin like `flutter_background_service`. 

1. Add the `flutter_background_service` plugin to your `pubspec.yaml` file and run `flutter pub get` to fetch the dependencies.

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_background_service: ^1.1.1
```

2. In your Dart code, import the `flutter_background_service` package and register the service as shown below:

```dart
import 'package:flutter_background_service/flutter_background_service.dart';

void main() {
  WidgetsFlutterBinding.ensureInitialized();
  FlutterBackgroundService.initialize(onStart);
}

void onStart() {
  // Start your background service here
}

```

3. To start the background service, call the `FlutterBackgroundService.start()` method.

```dart
void onStart() {
  FlutterBackgroundService.start();
  // Start your background service here
}
```

## Scheduling periodic updates

To schedule periodic updates, we can use the `android_alarm_manager` plugin.

1. Add the `android_alarm_manager` plugin to your `pubspec.yaml` file and run `flutter pub get`.

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_background_service: ^1.1.1
  android_alarm_manager: ^1.4.9
```

2. Import the `android_alarm_manager` package in your Dart code and schedule the task to run periodically.

```dart
import 'package:android_alarm_manager/android_alarm_manager.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await AndroidAlarmManager.initialize();
  await AndroidAlarmManager.periodic(
    const Duration(minutes: 30),
    0,
    fetchData,
    wakeup: true,
    rescheduleOnReboot: true,
  );
  runApp(MyApp());
}

void fetchData() {
  // Fetch your weather updates here
}
```

## Conclusion

By combining native platform code and Flutter plugins, we can run background services in a Flutter app to fetch weather updates or any other periodic data. With the right setup, our app can stay up-to-date with the latest information even when it's not actively being used.

## References

- Flutter: [https://flutter.dev](https://flutter.dev)
- flutter_background_service plugin: [https://pub.dev/packages/flutter_background_service](https://pub.dev/packages/flutter_background_service)
- android_alarm_manager plugin: [https://pub.dev/packages/android_alarm_manager](https://pub.dev/packages/android_alarm_manager)