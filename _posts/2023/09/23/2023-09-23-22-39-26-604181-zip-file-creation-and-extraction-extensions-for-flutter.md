---
layout: post
title: "Zip file creation and extraction extensions for Flutter"
description: " "
date: 2023-09-23
tags: [ZipFiles]
comments: true
share: true
---

If you are working with file compression and needs to create or extract zip files in a Flutter application, there are several extensions available that can simplify the process for you. In this blog post, we will explore two popular extensions for zip file creation and extraction in Flutter.

## 1. flutter_archive

`flutter_archive` is a powerful library that allows you to create and extract zip files in your Flutter application. It supports both compression and decompression of files.

To use `flutter_archive`, add the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_archive: ^2.0.0
```

Once you have added the dependency, you can create or extract zip files using the following code snippet:

```dart
import 'package:flutter_archive/flutter_archive.dart';

// Extracting a zip file
await FlutterArchive.extractToDirectory('path/to/zip/file', 'path/to/destination/directory');

// Creating a zip file
await FlutterArchive.zipDirectory(
  sourceDir: 'path/to/source/directory',
  zipFile: 'path/to/destination/zip/file',
);
```

With `flutter_archive`, you can easily extract or create zip files in your Flutter application.

## 2. path_provider and archive

Another approach to working with zip files in Flutter is to combine the `path_provider` and `archive` libraries. `path_provider` allows you to access the file system directories, while `archive` provides the functionality to create and extract zip files.

To use these libraries, add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  path_provider: ^2.0.5
  archive: ^3.1.2
```

Now, you can create or extract zip files using the following code snippet:

```dart
import 'dart:io';
import 'package:path_provider/path_provider.dart';
import 'package:archive/archive.dart';

// Extracting a zip file
String zipPath = 'path/to/zip/file';
String destinationPath = 'path/to/destination/directory';

Directory destinationDirectory = Directory(destinationPath);
if (!destinationDirectory.existsSync()) {
  destinationDirectory.createSync(recursive: true);
}

File zipFile = File(zipPath);
if (zipFile.existsSync()) {
  List<int> bytes = zipFile.readAsBytesSync();
  Archive archive = ZipDecoder().decodeBytes(bytes);

  for (ArchiveFile file in archive) {
    String filePath = '${destinationPath}/${file.name}';
    if (file.isFile) {
      List<int> data = file.content;
      File(filePath).writeAsBytesSync(data);
    } else {
      Directory(filePath).create(recursive: true);
    }
  }
}

// Creating a zip file
String sourcePath = 'path/to/source/directory';
String zipFilePath = 'path/to/destination/zip/file';

Directory sourceDirectory = Directory(sourcePath);
List<FileSystemEntity> files = sourceDirectory.listSync(recursive: true);

Archive archive = Archive();
for (FileSystemEntity file in files) {
  if (file is File) {
    String relativePath = file.path.substring(sourceDirectory.path.length);
    ArchiveFile archiveFile = ArchiveFile(relativePath, file.lengthSync(), await file.readAsBytes());
    archive.addFile(archiveFile);
  }
}

List<int> zipData = ZipEncoder().encode(archive);
File(zipFilePath).writeAsBytesSync(zipData);
```

By combining `path_provider` and `archive`, you can achieve zip file creation and extraction in your Flutter application.

These are two popular extensions that can help you create and extract zip files in a Flutter application. Choose the one that best suits your needs and integrate it into your project. Happy coding! #Flutter #ZipFiles