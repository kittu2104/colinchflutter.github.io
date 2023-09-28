---
layout: post
title: "Zip file creation and extraction extensions for Flutter"
description: " "
date: 2023-09-22
tags: [zipfiles]
comments: true
share: true
---

In Flutter, there are several packages available that provide functionality for creating and extracting zip files. These packages allow you to compress files into a zip archive or extract files from an existing zip archive, making it easy to work with zip files in your Flutter applications. In this blog post, we will discuss two popular zip file handling packages for Flutter.

## 1. `archive` package

The `archive` package is a lightweight and easy-to-use package that provides functionality for creating and manipulating zip archives in Flutter. It supports both zip file creation and extraction.

To create a zip file using the `archive` package, you can use the following example code:

```dart
import 'package:archive/archive.dart';

void createZipFile() {
  Archive archive = Archive();

  // Add files to the archive
  archive.addFile(ArchiveFile('file1.txt', 20, 'Hello World!'));
  archive.addFile(ArchiveFile('file2.txt', 15, 'Flutter is awesome!'));

  // Save the archive to a file
  File('my_archive.zip').writeAsBytesSync(ZipEncoder().encode(archive));
}
```
To extract files from a zip archive, you can use the following example code:

```dart
import 'package:archive/archive.dart';

void extractZipFile(String zipFilePath) {
  // Read the zip file
  final zipBytes = File(zipFilePath).readAsBytesSync();

  // Decode the zip file
  Archive archive = ZipDecoder().decodeBytes(zipBytes);

  // Extract files from the archive
  for (ArchiveFile file in archive) {
    File('extracted_files/${file.name}')
        .writeAsBytesSync(file.content as List<int>);
  }
}
```

## 2. `flutter_archive` package

The `flutter_archive` package is another popular choice for working with zip files in Flutter. It provides a simple and intuitive API for creating and extracting zip archives.

To create a zip file using the `flutter_archive` package, you can use the following example code:

```dart
import 'package:flutter_archive/flutter_archive.dart';

void createZipFile() async {
  // Create a list of files to be archived
  List<String> files = ['file1.txt', 'file2.txt'];

  // Create the zip file
  await ZipFile.createFromFiles(
    sourceDir: Directory.current.path,
    files: files,
    zipFile: 'my_archive.zip',
  );
}
```

To extract files from a zip archive, you can use the following example code:

```dart
import 'package:flutter_archive/flutter_archive.dart';

void extractZipFile(String zipFilePath) async {
  // Extract the zip file
  await ZipFile.extractToDirectory(
    zipFile: zipFilePath,
    destinationDir: Directory.current.path,
  );
}
```

## Conclusion

Both the `archive` package and the `flutter_archive` package provide useful functionality for handling zip files in Flutter. Depending on your specific requirements and preferences, you can choose the one that best suits your needs. With these packages, you can easily create and extract zip files, making it convenient to work with compressed files in your Flutter applications. 

#flutter #zipfiles