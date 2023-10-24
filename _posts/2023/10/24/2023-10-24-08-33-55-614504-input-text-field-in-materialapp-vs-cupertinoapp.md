---
layout: post
title: "Input text field in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: [text]
comments: true
share: true
---

When developing a mobile application, you can choose between the MaterialApp and CupertinoApp widgets provided by Flutter. These widgets offer different design styles for your app, including the input text fields. In this article, we will compare the input text field implementations in MaterialApp and CupertinoApp and highlight their differences.

## MaterialApp Input Text Field

In MaterialApp, the input text field widget is known as TextFormField. This widget is based on the Material Design guidelines and provides a classic text field with a underline-style border. You can customize various aspects of the TextFormField, including its decoration, validation, and input type.

Here is an example of using TextFormField in MaterialApp:

```dart
import 'package:flutter/material.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('MaterialApp Text Field'),
        ),
        body: Center(
          child: Padding(
            padding: EdgeInsets.all(20.0),
            child: TextFormField(
              decoration: InputDecoration(
                labelText: 'Username',
                hintText: 'Enter your username',
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

## CupertinoApp Input Text Field

On the other hand, if you prefer the sleek and modern iOS design style, you can use the CupertinoApp widget. In CupertinoApp, the input text field is called CupertinoTextField. This widget follows the Cupertino design guidelines and provides an input text field with a rounded border.

Here is an example of using CupertinoTextField in CupertinoApp:

```dart
import 'package:flutter/cupertino.dart';

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoApp(
      home: CupertinoPageScaffold(
        navigationBar: CupertinoNavigationBar(
          middle: Text('CupertinoApp Text Field'),
        ),
        child: Center(
          child: Padding(
            padding: EdgeInsets.all(20.0),
            child: CupertinoTextField(
              placeholder: 'Enter your username',
            ),
          ),
        ),
      ),
    );
  }
}
```

## Conclusion

In summary, when it comes to input text fields, MaterialApp offers a classic Material Design style with a underline-style border, while CupertinoApp provides a sleek rounded input text field conforming to the iOS design guidelines. Choose the one that suits your app's design requirements and platform consistency.

#flutter #text-field