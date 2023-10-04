---
layout: post
title: "Implementing database backup and restore in scheduled tasks with WorkManager for Flutter"
description: " "
date: 2023-10-01
tags: [WorkManager]
comments: true
share: true
---

In many mobile applications, it's crucial to have a backup mechanism in place for the app's data, especially when dealing with databases. This ensures that user data is not lost in the event of device failure or data corruption. In this blog post, we will explore how to implement database backup and restore functionality in a Flutter app using scheduled tasks with WorkManager.

## What is WorkManager?

WorkManager is an Android library that enables you to schedule tasks and ensure they execute even if the app is closed or the device is rebooted. It provides a flexible, battery-friendly API for running background tasks in a way that maximizes efficiency and minimizes impact on device performance.

## Prerequisites

Before diving into the implementation process, make sure you have the following:

- Flutter SDK installed on your machine
- Flutter project set up

## 1. Integrating WorkManager in Flutter

To utilize WorkManager in our Flutter project, we need to include the necessary dependencies.

1. Open your `pubspec.yaml` file and add the following lines under the `dependencies` section:

   ```yaml
   dependencies:
     workmanager: ^0.4.0-nullsafety
     flutter_local_notifications: ^5.0.0+1
     path_provider: ^2.0.1
     shared_preferences: ^2.0.5
   ```

   Here, we are including the WorkManager, flutter_local_notifications, path_provider, and shared_preferences packages.

2. Run `flutter pub get` to fetch the dependencies.

## 2. Setting Up Database Backup and Restore Tasks

Now let's create the tasks responsible for backing up and restoring the database.

### Backup Task

1. Create a new Dart file, such as `backup_task.dart`, and define the `backupDatabase` function. This function will handle the backup logic.

   ```dart
   import 'package:path/path.dart' as path;
   import 'package:path_provider/path_provider.dart';
   import 'package:shared_preferences/shared_preferences.dart';
   
   Future<void> backupDatabase() async {
     // Get the path to the database file
     final databasesPath = await getDatabasesPath();
     final sourcePath = path.join(databasesPath!, 'your_database_name.db');
   
     // Create a backup directory in the app's documents directory
     final appDocumentsDirectory = await getApplicationDocumentsDirectory();
     final backupPath = path.join(appDocumentsDirectory.path, 'backup');
     final directory = await Directory(backupPath).create(recursive: true);
   
     // Generate a unique backup file name using the current timestamp
     final backupFile = File(path.join(directory.path, 'backup_${DateTime.now().millisecondsSinceEpoch}.db'));
   
     // Create a copy of the database file in the backup directory
     await File(sourcePath).copy(backupFile.path);
   
     // Store the backup file path in SharedPreferences
     final preferences = await SharedPreferences.getInstance();
     preferences.setString('backupPath', backupFile.path);
   }
   ```

   This function retrieves the path to the database file, creates a backup directory if it doesn't exist, generates a unique backup file name using the current timestamp, copies the database file to the backup directory, and stores the backup file path in `SharedPreferences`.

### Restore Task

1. Create another Dart file, such as `restore_task.dart`, and define the `restoreDatabase` function. This function will handle the restore logic.

   ```dart
   import 'package:path_provider/path_provider.dart';
   import 'package:shared_preferences/shared_preferences.dart';
   
   Future<void> restoreDatabase() async {
     // Get the backup file path from SharedPreferences
     final preferences = await SharedPreferences.getInstance();
     final backupPath = preferences.getString('backupPath');
   
     if (backupPath != null) {
       // Get the path to the database file
       final databasesPath = await getDatabasesPath();
       final destinationPath = path.join(databasesPath!, 'your_database_name.db');
   
       // Copy the backup file to the database file location
       await File(backupPath).copy(destinationPath);
     } else {
       // Handle the case when no backup file exists
       // or the backupPath value is missing
     }
   }
   ```

   This function retrieves the backup file path from `SharedPreferences` and checks if it exists. If a backup file is found, it copies the file to the original database file location.

## 3. Scheduling Backup and Restore Tasks

Now that we have defined backup and restore tasks, let's schedule them to run periodically using WorkManager.

### Scheduling Backup Task

1. Open the `main.dart` file of your Flutter project.

2. Import the necessary packages:

   ```dart
   import 'package:workmanager/workmanager.dart';
   import 'package:your_app_name/backup_task.dart';
   ```

3. Initialize WorkManager in the `main` function:

   ```dart
   void main() {
     WidgetsFlutterBinding.ensureInitialized();
     Workmanager.initialize(callbackDispatcher);
     Workmanager.registerPeriodicTask(
       'backupTask',
       'backupTask',
       frequency: const Duration(days: 1),
     );
     runApp(MyApp());
   }
   ```

   Here, we are initializing WorkManager using the `callbackDispatcher` as the callback dispatcher function. We also register a periodic task named `'backupTask'` to run every 24 hours.

4. Create a new file called `callback_dispatcher.dart`. 

   ```dart
   import 'package:workmanager/workmanager.dart';
   import 'package:your_app_name/backup_task.dart';
   import 'package:your_app_name/restore_task.dart';
   
   void callbackDispatcher() {
     Workmanager.executeTask((String? taskName, inputData) {
       switch (taskName) {
         case 'backupTask':
           backupDatabase();
           break;
         case 'restoreTask':
           restoreDatabase();
           break;
       }
       return Future.value(true);
     });
   }
   ```

   This function executes different tasks based on their names. In this case, it runs `backupDatabase()` for `'backupTask'` and `restoreDatabase()` for `'restoreTask'`.

5. Build and run your Flutter application. The backup task will be automatically scheduled to run every 24 hours.

### Scheduling Restore Task

To schedule the restore task, we need to trigger it manually. For example, you can provide a button in your app's UI that allows users to restore their database.

1. When the restore button is pressed, call the following code to schedule the restore task immediately:

   ```dart
   Workmanager.registerOneOffTask(
     'restoreTask',
     'restoreTask',
     inputData: {},
   );
   ```

   This code schedules a one-off task named `'restoreTask'` to run immediately.

## Conclusion

By implementing database backup and restore functionality in scheduled tasks with WorkManager for Flutter, you can ensure that your app's data is regularly backed up and can be restored when needed. This will provide a seamless user experience and protect user data from potential loss or corruption.

#Flutter #WorkManager