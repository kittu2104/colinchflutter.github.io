---
layout: post
title: "Implementing state restoration with PDF rendering in Flutter"
description: " "
date: 2023-09-15
tags: [PDFRendering]
comments: true
share: true
---

In Flutter, state restoration is a powerful feature that allows you to preserve the state of your app across sessions and device restarts. This is particularly useful when working with apps that involve complex user interactions or require the restoration of specific data.

In this blog post, we will walk you through the process of implementing state restoration in a Flutter app that involves PDF rendering. We will assume you have a basic understanding of Flutter and have already set up a Flutter project.

## Step 1: Add Dependencies

To get started, you'll need to add the necessary dependencies to your `pubspec.yaml` file. Open the file and add the following lines under the `dependencies` section:

```yaml
dependencies:
  flutter:
    sdk: flutter
  pdf_render: ^1.0.0
```

Run `flutter pub get` in your terminal to download the new packages.

## Step 2: Set Up State Restoration

In order to enable state restoration in your app, you need to initialise it in your main function. Open `lib/main.dart` and modify the `main` function as follows:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final RouteInformationParser<Object> _routeInformationParser =
      _MyRouteInformationParser();

  final RouteInformationProvider _routeInformationProvider =
      RouteInformationProvider();

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      title: 'PDF Viewer',
      routerDelegate: RouterDelegate(
        routeInformationProvider: _routeInformationProvider,
        routeInformationParser: _routeInformationParser,
      ),
      routeInformationProvider: _routeInformationProvider,
      routeInformationParser: _routeInformationParser,
      restorationScopeId: 'app',
      debugShowCheckedModeBanner: false,
    );
  }
}

class _MyRouteInformationParser extends RouteInformationParser<Object> {
  @override
  Future<Object> parseRouteInformation(
      RouteInformation routeInformation) async {
    return Object(); // Replace `Object` with your actual state object
  }

  @override
  RouteInformation restoreRouteInformation(Object configuration) {
    return RouteInformation(location: ''); // Replace the empty string with your actual location
  }
}
```

In the code above, we set up a custom `RouteInformationParser` and use a custom `RouterDelegate` to handle the routing and state restoration of our app. Make sure to replace the `Object` placeholder with your actual state object and location.

## Step 3: Implement PDF Rendering

To demonstrate state restoration with PDF rendering, let's build a basic PDF viewer. Create a new file `lib/pdf_viewer.dart` and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:pdf_render/pdf_render.dart';

class PDFViewer extends StatefulWidget {
  @override
  _PDFViewerState createState() => _PDFViewerState();
}

class _PDFViewerState extends State<PDFViewer> {
  PdfDocument? _document;

  @override
  void initState() {
    super.initState();
    _loadDocument();
  }

  void _loadDocument() async {
    final document = await PdfDocument.openAsset('assets/sample.pdf');
    setState(() {
      _document = document;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('PDF Viewer'),
      ),
      body: _document != null
          ? PdfPageView(
              document: _document!,
              onPageChanged: (int page) {
                print('Page changed to: $page');
              },
            )
          : Center(
              child: CircularProgressIndicator(),
            ),
    );
  }
}
```

In the code above, we create a `PDFViewer` widget that loads a PDF document from the assets folder using the `PdfDocument` class from the `pdf_render` package. Replace `'assets/sample.pdf'` with the path to your own PDF file.

## Step 4: Update Router Definitions

Finally, we need to update our router definitions to include the PDF viewer route. Open `lib/main.dart` and modify the `_MyRouteInformationParser` class as follows:

```dart
class _MyRouteInformationParser extends RouteInformationParser<Object> {
  @override
  Future<Object> parseRouteInformation(
      RouteInformation routeInformation) async {
    final uri = Uri.parse(routeInformation.location!);
    if (uri.path == '/pdf-viewer') {
      return PDFViewer(); // Replace `PDFViewer` with your actual viewer widget
    }
    return Object(); // Replace `Object` with your actual state object
  }

  @override
  RouteInformation restoreRouteInformation(Object configuration) {
    if (configuration is PDFViewer) {
      return RouteInformation(location: '/pdf-viewer');
    }
    return RouteInformation(location: ''); // Replace the empty string with your actual location
  }
}
```

In the code above, we add a condition to check if the requested route is `/pdf-viewer` and return the `PDFViewer` widget if it is. Make sure to replace `PDFViewer` with your actual viewer widget.

## Conclusion

Congratulations! You have successfully implemented state restoration with PDF rendering in your Flutter app. With this feature, your app will be able to preserve the state of the PDF viewer, allowing users to resume their reading seamlessly even after restarting the app or device.

Remember to add the necessary `#Flutter` and `#PDFRendering` hashtags to make your blog post searchable and discoverable.