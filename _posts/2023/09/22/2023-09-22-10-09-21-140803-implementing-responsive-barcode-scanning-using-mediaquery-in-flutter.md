---
layout: post
title: "Implementing responsive barcode scanning using `MediaQuery` in Flutter"
description: " "
date: 2023-09-22
tags: [ff6666]
comments: true
share: true
---

Barcode scanning has become an integral part of many mobile applications. With Flutter, it is possible to implement barcode scanning functionality that can adapt to different screen sizes and orientations. One way to achieve this is by using the `MediaQuery` class, which allows us to determine the properties of the device's screen.

## Setting Up the Project

Before we proceed, make sure you have Flutter installed and set up on your machine. Once you have that ready, create a new Flutter project by running the following command:

```dart
flutter create responsive_barcode_scanning
```

Navigate to the project folder:

```dart
cd responsive_barcode_scanning
```

Open the project in your favorite code editor.

## Implementing Barcode Scanning

To implement barcode scanning in Flutter, we'll be using a package called `flutter_barcode_scanner`. Start by adding the package dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter
  flutter_barcode_scanner: ^2.0.0
```

Run the following command to fetch the package:

```dart
flutter pub get
```

Next, open up your main Dart file (usually `lib/main.dart`) and import the necessary packages:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_barcode_scanner/flutter_barcode_scanner.dart';
```

Create a new `StatefulWidget` class called `BarcodeScannerScreen`. This class will hold the logic for scanning barcodes and display the results on the screen:

```dart
class BarcodeScannerScreen extends StatefulWidget {
  @override
  _BarcodeScannerScreenState createState() => _BarcodeScannerScreenState();
}

class _BarcodeScannerScreenState extends State<BarcodeScannerScreen> {
  String _barcodeResult = '';

  Future<void> _scanBarcode() async {
    String barcodeResult = await FlutterBarcodeScanner.scanBarcode(
      '#ff6666', // Color of the toolbar
      'Cancel', // Text for the button to cancel scanning
    );

    setState(() {
      _barcodeResult = barcodeResult;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Barcode Scanner'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Scan Result:', style: TextStyle(fontSize: 24)),
            SizedBox(height: 16),
            Text(_barcodeResult, style: TextStyle(fontSize: 18)),
            SizedBox(height: 16),
            ElevatedButton(
              onPressed: _scanBarcode,
              child: Text('Scan Barcode'),
            ),
          ],
        ),
      ),
    );
  }
}
```

The above code defines a `BarcodeScannerScreen` that displays the scanning result, along with a button to initiate the scanning process using the `FlutterBarcodeScanner` package.

Now, update the `main` function to use the `BarcodeScannerScreen` as the main widget:

```dart
void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Responsive Barcode Scanning',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: BarcodeScannerScreen(),
    );
  }
}
```

## Making the App Responsive

To make the barcode scanning app responsive, we can utilize the `MediaQuery` class provided by Flutter. This class allows us to access the device's screen dimensions and adapt our UI accordingly.

Wrap the `Column` widget inside a `LayoutBuilder` widget, which provides the constraints of the parent widget. We can then use these constraints to adjust the font sizes and button sizes accordingly:

```dart
LayoutBuilder(
  builder: (BuildContext context, BoxConstraints constraints) {
    return Column(
      mainAxisAlignment: MainAxisAlignment.center,
      children: [
       Text('Scan Result:', style: TextStyle(fontSize: constraints.maxHeight * 0.04)),
       SizedBox(height: constraints.maxHeight * 0.02),
       Text(_barcodeResult, style: TextStyle(fontSize: constraints.maxHeight * 0.03)),
       SizedBox(height: constraints.maxHeight * 0.02),
       ElevatedButton(
         onPressed: _scanBarcode,
         child: Padding(
           padding: EdgeInsets.symmetric(
             horizontal: constraints.maxWidth * 0.05,
             vertical: constraints.maxHeight * 0.02,
           ),
           child: Text('Scan Barcode', style: TextStyle(fontSize: constraints.maxHeight * 0.03)),
         ),
       ),
     ],
   );
 },
)
```

In the above code snippet, we are adjusting the font sizes and button sizes relative to the screen height and width. This allows the UI to adapt to different devices and screen sizes, ensuring a consistent and responsive user experience.

## Conclusion

In this tutorial, we learned how to implement responsive barcode scanning in Flutter using the `MediaQuery` class. By utilizing the device's screen dimensions, we can adapt our UI elements to provide a seamless scanning experience across different screen sizes and orientations.

Now you can incorporate responsive barcode scanning into your Flutter applications and deliver a user-friendly experience on various devices!

#flutter #barcode-scanning