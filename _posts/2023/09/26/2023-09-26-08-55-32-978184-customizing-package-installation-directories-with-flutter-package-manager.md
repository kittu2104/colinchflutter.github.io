---
layout: post
title: "Customizing package installation directories with Flutter Package Manager"
description: " "
date: 2023-09-26
tags: [flutter, package]
comments: true
share: true
---

Flutter package manager provides a streamlined approach to managing and installing packages in your Flutter projects. By default, when you install a package, it gets stored in the `pub-cache` directory within your Flutter SDK installation. However, there may be scenarios where you want to customize the location where packages are installed. In this blog post, we will explore how to customize package installation directories with Flutter package manager.

## Option 1: Specifying the Installation Directory in pubspec.yaml

One way to customize the package installation directory is to specify it directly in the `pubspec.yaml` file of your Flutter project. To do this, add the following lines to your `pubspec.yaml`:

```yaml
flutter:
  packages:
    directory: path/to/custom_directory
```

Replace `path/to/custom_directory` with the desired path where you want the packages to be installed. 

Save the `pubspec.yaml` file and run `flutter pub get` to install packages. The packages will now be downloaded and stored in the specified custom directory.

## Option 2: Setting the FLUTTER_PACKAGE_MANAGER environment variable

Another approach to customize the package installation directory is by setting the `FLUTTER_PACKAGE_MANAGER` environment variable. This method allows you to define the package installation directory globally, applicable to all Flutter projects on your system.

On Linux/Mac:

```bash
export FLUTTER_PACKAGE_MANAGER=path/to/custom_directory
```

On Windows:

```bash
set FLUTTER_PACKAGE_MANAGER=path/to/custom_directory
```

Replace `path/to/custom_directory` with the desired path where you want the packages to be installed.

After setting the environment variable, open a new terminal window or restart your IDE for the changes to take effect. Now, when you run `flutter pub get`, the packages will be installed in the specified custom directory.

## Conclusion

Customizing package installation directories with Flutter package manager gives you more flexibility in managing your packages. By specifying the installation directory in `pubspec.yaml` or setting the `FLUTTER_PACKAGE_MANAGER` environment variable, you can easily control where packages are installed in your Flutter projects.

#flutter #package #manager #customization