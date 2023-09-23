---
layout: post
title: "Implementing file handling in Flutter WebAssembly"
description: " "
date: 2023-09-24
tags: [Flutter, WebAssembly]
comments: true
share: true
---

Flutter WebAssembly is a powerful framework for building web applications using the Flutter SDK. While it provides a vast array of features for web development, native file handling is not directly supported out of the box. However, there are ways to implement file handling functionality in Flutter WebAssembly by leveraging the capabilities of JavaScript.

To implement file handling in Flutter WebAssembly, we can use JavaScript interop provided by the `dart:js` library. This allows us to interact with JavaScript code from within our Flutter application.

Here's a step-by-step guide to implementing file handling in Flutter WebAssembly:

## 1. Set Up the Project

Start by creating a new Flutter project, specifically targeting the web platform. You can use the following command:

```shell
flutter create file_handling_flutter_web
flutter run -d chrome
```

This will create a new Flutter web project and run it in the Chrome browser.

## 2. Create JavaScript Wrapper Functions

Next, we need to create JavaScript functions that will perform the file handling operations for us. Let's start by creating a JavaScript file called `file_handling.js` in the `web` directory of your Flutter project.

In `file_handling.js`, define functions for reading and writing files. For example:

```javascript
// file_handling.js

function readTextFile(file, callback) {
  const reader = new FileReader();
  reader.onload = function (e) {
    callback(e.target.result);
  };
  reader.readAsText(file);
}

function writeTextFile(filename, content) {
  const blob = new Blob([content], { type: 'text/plain' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = filename;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
}
```

These functions use the FileReader API to read a file and the Blob API to write a file.

## 3. Import JavaScript Functions in Flutter

To use these JavaScript functions in Flutter, we need to import them using `dart:js`.

Create a new Dart file called `file_handling.dart` in the `lib` directory of your Flutter project. In that file, import `dart:js` and declare externs for the JavaScript functions:

```dart
// file_handling.dart

import 'dart:js' as js;

void readTextFile(js.JsObject file, Function(String) callback) {
  js.context.callMethod('readTextFile', [file, callback]);
}

void writeTextFile(String filename, String content) {
  js.context.callMethod('writeTextFile', [filename, content]);
}
```

Here, we are declaring two Dart wrapper functions that call the respective JavaScript functions using `dart:js`.

## 4. Implement File Handling Logic

Now, it's time to implement file handling logic in your Flutter application.

First, add a button to the UI that allows the user to select a file for reading:

```dart
import 'package:flutter/material.dart';
import 'package:file_handling_flutter_web/file_handling.dart' as fileHandling;

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'File Handling in Flutter Web',
      theme: ThemeData(primarySwatch: Colors.blue),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('File Handling in Flutter Web'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            RaisedButton(
              child: Text('Select File'),
              onPressed: () {
                selectFile();
              },
            ),
          ],
        ),
      ),
    );
  }

  void selectFile() async {
    final fileInput = html.FileUploadInputElement();
    fileInput.click();
    await fileInput.onChange.first;
    final file = fileInput.files.first;
    readTextFile(file, (contents) {
      print(contents);
    });
  }
}
```

In the `selectFile` method, we create a file input element and trigger its click event. We then wait for the file to be selected by the user and pass it to the `readTextFile` function.

Next, let's add a button to save a text file:

```dart
class MyHomePage extends StatelessWidget {
  // ...

  void saveFile() {
    final content = 'Hello, World!';
    writeTextFile('output.txt', content);
  }

  @override
  Widget build(BuildContext context) {
    // ...
          children: [
            RaisedButton(
              child: Text('Select File'),
              onPressed: () {
                selectFile();
              },
            ),
            RaisedButton(
              child: Text('Save File'),
              onPressed: () {
                saveFile();
              },
            ),
          ],
    // ...
  }
}
```

In the `saveFile` method, we simply call the `writeTextFile` function with a filename and content.

## 5. Test the Code

Now, you can run your Flutter web application and test the file handling feature. Select a file using the "Select File" button, and it will be read and printed to the console. Click the "Save File" button, and a file named "output.txt" will be downloaded, containing the text "Hello, World!".

Congratulations! You have successfully implemented file handling in Flutter WebAssembly using JavaScript interop.

#Flutter #WebAssembly