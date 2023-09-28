---
layout: post
title: "Generating documentation for custom packages with Flutter Package Manager"
description: " "
date: 2023-09-26
tags: [Documentation]
comments: true
share: true
---

As developers, we often find ourselves working on custom packages in Flutter to keep our codebase modular and organized. Documenting these packages is crucial for maintaining a clear understanding of their functionality and usage. One way to generate documentation for our custom packages is by utilizing the Flutter Package Manager.

## What is Flutter Package Manager?

Flutter Package Manager is a command-line tool that helps with the management of Flutter packages in your project. It provides various features, and one of them is the ability to generate documentation for custom packages.

## Steps to Generate Documentation

To generate documentation for your custom package, follow these steps:

1. **Install Flutter Package Manager:** If you haven't installed the Flutter Package Manager yet, run the following command in your terminal:

```bash
$ flutter pub global activate fpm
```

2. **Navigate to your package directory:** Open your terminal and navigate to the directory where your custom package is located.

3. **Generate the documentation:** Run the following command to generate the documentation for your custom package:

```bash
$ flutter pub global run fpm dartdoc
```

4. **Access the generated documentation:** Once the documentation generation is complete, you can access it in the `doc` folder inside your custom package's directory.

## Customizing the Documentation

You can customize the generated documentation by modifying the `pubspec.yaml` file in your custom package. Within the file, you can specify the `dartdoc_options` under the `flutter` section. For example:

```yaml
flutter:
  dartdoc_options:
    exclude: ['**/example/**'] # Exclude example folder from documentation
```

In the above example, we've excluded the `example` folder from being included in the generated documentation. You can customize the `dartdoc_options` to meet your specific requirements.

## Conclusion

Generating documentation for custom packages with Flutter Package Manager is a straightforward process that greatly improves code maintainability and collaboration. By following the steps outlined in this blog post, you can easily generate and customize documentation for your custom packages, ensuring a clear understanding of their functionality and usage.

#Flutter #Documentation