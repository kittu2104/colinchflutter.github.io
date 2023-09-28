---
layout: post
title: "Using local packages with Flutter Package Manager"
description: " "
date: 2023-09-26
tags: [LocalPackages]
comments: true
share: true
---

## Introduction
Flutter provides a convenient package manager that allows you to easily add external dependencies to your project. However, there may be situations where you want to use a local package that has not been published on a package repository. In this blog post, we will explore how to use local packages with the Flutter package manager.

## Step 1: Create your Local Package
The first step is to create your local package. You can do this by running the following command in your terminal:

```bash
flutter create --template=package local_package
```

This will create a new Flutter package named `local_package` in the current directory. You can then navigate into the `local_package` directory using `cd local_package`.

## Step 2: Add Local Package as a Dependency
To use the `local_package` in your Flutter project, you need to add it as a dependency. Open the `pubspec.yaml` file in your main project directory and add the following lines:

```yaml
dependencies:
  local_package:
    path: ../local_package
```

In the above code, `local_package` is the name of the package and `path` is the relative path to the package directory.

## Step 3: Update Dependencies
After adding the local package dependency, you need to update the dependencies using the Flutter package manager. Run the following command in your terminal:

```bash
flutter pub get
```

This will fetch the local package and update the project dependencies.

## Step 4: Import and Use Local Package
Now that you have added the local package as a dependency, you can import and use it in your Flutter project. Import the local package in your Dart file as follows:

```dart
import 'package:local_package/local_package.dart';
```

You can then use the classes, functions, or variables declared in the local package in your project code.

## Conclusion
Using local packages with the Flutter package manager is straightforward and allows you to easily reuse code across multiple projects. By following the steps outlined in this blog post, you can add and use local packages in your Flutter projects seamlessly.

#Flutter #LocalPackages