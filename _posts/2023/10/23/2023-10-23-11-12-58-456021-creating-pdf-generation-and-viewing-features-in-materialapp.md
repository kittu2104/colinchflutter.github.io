---
layout: post
title: "Creating PDF generation and viewing features in MaterialApp."
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In this blog post, we will explore how to incorporate PDF generation and viewing capabilities into your MaterialApp using popular Flutter packages. Generating and viewing PDF files can be extremely useful in various scenarios, such as generating invoices, generating reports, or simply displaying PDF documents within your application.

To implement these features, we will be using two popular Flutter packages:

1. **pdf** package: This package allows us to generate PDF documents from scratch or modify existing PDF files.

2. **flutter_pdfview** package: This package provides a widget that allows us to view PDF files within our MaterialApp.

Let's dive into the implementation details!

## Generating PDF Documents

To generate PDF documents, we will use the **pdf** package. You can add this package to your `pubspec.yaml` file:

```yaml
dependencies:
  pdf: ^<latest_version>
```

Once you have added the package, you can start generating PDF documents using the provided classes and utilities.

Here's an example of how you can generate a simple PDF document:

```dart
import 'package:pdf/pdf.dart';
import 'package:pdf/widgets.dart' as pw;

class PdfGenerator {
  static pw.Document generatePdf() {
    final pdf = pw.Document();

    pdf.addPage(
      pw.Page(
        build: (pw.Context context) {
          return pw.Center(
            child: pw.Text('Hello, PDF World!', style: pw.TextStyle(fontSize: 24))
          );
        },
      ),
    );

    return pdf;
  }
}
```

In this example, we create a `pw.Document` object and add a page with a centered text widget. You can customize the PDF document further by adding more pages, different widgets, or even images.

## Viewing PDF Documents

To view PDF documents within our MaterialApp, we will make use of the **flutter_pdfview** package. Add this package to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_pdfview: ^<latest_version>
```

After adding the package, you can utilize the provided `PDFView` widget to display PDF files within your MaterialApp.

Here's an example of how you can implement the PDF viewing feature:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_pdfview/flutter_pdfview.dart';

class PdfViewerScreen extends StatefulWidget {
  final String pdfPath;

  const PdfViewerScreen({required this.pdfPath});

  @override
  _PdfViewerScreenState createState() => _PdfViewerScreenState();
}

class _PdfViewerScreenState extends State<PdfViewerScreen> {
  late int pageCount = 0;
  late int currentPage = 0;

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('PDF Viewer'),
      ),
      body: PDFView(
        filePath: widget.pdfPath,
        onPageChanged: (int page, int total) {
          setState(() {
            currentPage = page;
            pageCount = total;
          });
        },
      ),
      bottomNavigationBar: BottomAppBar(
        child: Padding(
          padding: EdgeInsets.all(16.0),
          child: Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text('Page $currentPage of $pageCount'),
            ],
          ),
        ),
      ),
    );
  }
}
```

In this example, we create a stateful widget called `PdfViewerScreen` that takes the path of the PDF file as a parameter. The `PDFView` widget is used to display the PDF file, and the `onPageChanged` callback is used to update the current page and total page count.

You can navigate to the `PdfViewerScreen` and pass the path of the PDF file you want to view.

## Conclusion

In this blog post, we have explored how to incorporate PDF generation and viewing features into your MaterialApp using the **pdf** and **flutter_pdfview** packages. With these packages, you can generate custom PDF documents and seamlessly view PDF files within your Flutter application.

By combining the PDF generation and viewing features, you can enhance the functionality of your MaterialApp and provide a richer user experience.

Make sure to check the official documentation of the **pdf** and **flutter_pdfview** packages for more information and advanced usage.

Happy PDF generation and viewing! 📄

> Tags: #Flutter #PDF