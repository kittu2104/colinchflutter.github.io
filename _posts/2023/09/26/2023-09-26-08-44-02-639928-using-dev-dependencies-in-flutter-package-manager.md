---
layout: post
title: "Using dev dependencies in Flutter Package Manager"
description: " "
date: 2023-09-26
tags: [flutter, devdependencies]
comments: true
share: true
---

Dev dependencies are dependencies that are only required during development, but not when the package is being used. These dependencies are typically used for testing frameworks, code formatting, or other developer tools.

To specify a dev dependency in your Flutter package, you need to update the `pubspec.yaml` file. Inside the `dependencies` section, you can add a `dev_dependencies` subsection where you can list your dev dependencies.

Here's an example of how to specify dev dependencies in `pubspec.yaml`:

```yaml
dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^1.0.0
  pedantic: ^1.0.0
```

In this example, we are adding three dev dependencies:

1. `flutter_test`: This is the Flutter testing framework that allows you to write and execute tests for your package.
2. `flutter_lints`: This package provides lint rules for Dart and Flutter. It helps you enforce coding style and best practices.
3. `pedantic`: This package provides additional lints and static analysis for your Dart code. It helps you write more consistent and maintainable code.

To install the dev dependencies, you need to run the following command in the root directory of your Flutter package:

```bash
flutter pub get --dev
```

Adding the `--dev` flag ensures that only dev dependencies are installed.

Using dev dependencies in your Flutter package allows you to separate development-specific tools and libraries from the regular dependencies. It keeps your production codebase clean and ensures that your package doesn't have unnecessary dependencies when used by other projects.

Remember to **run tests and check for linting issues** with your dev dependencies to catch any potential bugs or issues before publishing your package.

#flutter #pub #devdependencies