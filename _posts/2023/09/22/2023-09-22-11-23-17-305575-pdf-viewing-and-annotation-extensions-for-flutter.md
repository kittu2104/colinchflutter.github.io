---
layout: post
title: "PDF viewing and annotation extensions for Flutter"
description: " "
date: 2023-09-22
tags: [extensions]
comments: true
share: true
---

Flutter is a powerful cross-platform framework for building beautiful and performant mobile applications. If you're looking to incorporate PDF viewing and annotation capabilities into your Flutter app, you're in luck! There are several excellent extensions available that can help you achieve this functionality. In this blog post, we will explore two popular PDF extensions for Flutter: **pdf_flutter** and **flutter_pdfview**.

## 1. pdf_flutter

**pdf_flutter** is a comprehensive Flutter extension that allows you to view and interact with PDF files in your app. This extension provides a set of widgets and classes that make it easy to integrate PDF viewing and annotation features. To get started, you can add the **pdf_flutter** package to your `pubspec.yaml` file:

```yaml
dependencies:
  pdf_flutter: ^1.0.0
```

With **pdf_flutter**, you can display PDF documents using the `PDFViewer` widget. This widget provides a customizable UI for navigating through pages, zooming, and searching within the PDF. Additionally, you can use the `PDFAnnotator` widget to enable annotation capabilities, allowing users to highlight text, add comments, and draw on the PDF.

```dart
import 'package:pdf_flutter/pdf_flutter.dart';

PDFViewer(
  document: PDFDocument.fromAsset('assets/document.pdf'),
  showNavigation: true,
  showPicker: true,
  viewerActions: [
    IfOnPageAction(),
    GoToFirstPageAction(),
    PreviousPageAction(),
    NextPageAction(),
    GoToLastPageAction(),
    ZoomOutAction(),
    ZoomInAction(),
    ShareAction(),
  ],
)


PDFAnnotator(
  document: PDFDocument.fromAsset('assets/document.pdf'),
  onPageChanged: (int page) {
    // Handle page change event
  },
)
```

## 2. flutter_pdfview

Another popular extension for PDF viewing in Flutter is **flutter_pdfview**. This extension provides a simple and efficient way to display PDF files within your app. To start using **flutter_pdfview**, add it to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_pdfview: ^1.0.0
```

Using **flutter_pdfview**, you can render PDF documents using the `PDFView` widget. This widget allows you to customize the display options such as page spacing, background color, and initial page number. You can also listen for events like page change and document load completion.

```dart
import 'package:flutter_pdfview/flutter_pdfview.dart';

PDFView(
  filePath: 'path/to/document.pdf',
  pageNumber: 1,
  onPageChanged: (int page, int total) {
    // Handle page change event
  },
  onViewCreated: (PDFViewController controller) {
    // Access the PDF controller
  },
)
```

## Conclusion

Adding PDF viewing and annotation capabilities to your Flutter app has never been easier. With the help of extensions like **pdf_flutter** and **flutter_pdfview**, you can enhance your app's functionality and provide a seamless PDF experience for your users.

Don't forget to check the official documentation and explore further options and customization features offered by these extensions.

#pdf #flutter #extensions