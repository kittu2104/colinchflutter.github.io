---
layout: post
title: "Implementing network requests in scheduled tasks with WorkManager in Flutter"
description: " "
date: 2023-10-01
tags: [Flutter, WorkManager]
comments: true
share: true
---

In Flutter, WorkManager is a powerful library that allows you to schedule and execute background tasks, such as network requests, even when your app is not actively running. With WorkManager, you can perform these tasks at predefined intervals or in response to specific triggers. In this blog post, we will explore how to use WorkManager to schedule and execute network requests in Flutter.

## Getting started with WorkManager

To get started, you need to add the WorkManager package to your Flutter project. Open the `pubspec.yaml` file and add the following dependency:

```dart
dependencies:
  workmanager: ^0.4.1
```

After adding the dependency, run `flutter pub get` to fetch the package.

## Scheduling a network request

To schedule a network request, you need to define a function that will be executed when the task is triggered. Let's create a function named `performNetworkRequest` that will make a GET request to a remote server using the `http` package:

```dart
import 'package:http/http.dart' as http;

void performNetworkRequest() async {
  var url = Uri.parse('https://api.example.com/data');
  var response = await http.get(url);

  if (response.statusCode == 200) {
    // Process the response data here
  } else {
    // Handle the error
  }
}
```

Next, you can use the `WorkManager` class to schedule the network request. Let's schedule the task to run every 5 minutes:

```dart
import 'package:workmanager/workmanager.dart';

void main() {
  Workmanager.initialize(
    callbackDispatcher,
    isInDebugMode: false,
  );
  Workmanager.registerPeriodicTask(
    'network_request_task',
    'network_request_task',
    inputData: {},
    frequency: Duration(minutes: 5),
  );
}

void callbackDispatcher() {
  Workmanager.executeTask((task, inputData) {
    performNetworkRequest();
    return Future.value(true);
  });
}
```

In the above code, `Workmanager.initialize` sets up the WorkManager library, and `Workmanager.registerPeriodicTask` schedules the task to run periodically. The `callbackDispatcher` function is called when the task is triggered, and it simply calls the `performNetworkRequest` function.

## Handling errors and retries

When performing network requests in scheduled tasks, it is essential to handle errors gracefully and implement retry mechanisms to ensure data consistency. To handle errors and retries, you can modify the `performNetworkRequest` function as follows:

```dart
import 'package:http/http.dart' as http;

void performNetworkRequest() async {
  var url = Uri.parse('https://api.example.com/data');
  var response = await http.get(url);

  if (response.statusCode == 200) {
    // Process the response data here
  } else if (response.statusCode == 429) {
    // API rate limit exceeded, retry after 1 minute
    Workmanager.registerOneOffTask(
      'network_request_task',
      'network_request_task',
      initialDelay: Duration(minutes: 1),
    );
  } else {
    // Handle other HTTP errors
  }
}
```

In the updated code, if the API returns a rate limit exceeded error (status code 429), we can use `Workmanager.registerOneOffTask` to reschedule the task after a delay of 1 minute. This ensures that the subsequent retry request is made after the rate limit is reset.

## Conclusion

In this blog post, we have seen how to leverage WorkManager to schedule and execute network requests in Flutter. With WorkManager, you can perform background tasks reliably and efficiently, even when your app is not actively running. By handling errors and implementing retry mechanisms, you can ensure the smooth functioning of your network requests in scheduled tasks.

#Flutter #WorkManager