---
layout: post
title: "Implementing responsive barcode scanning using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [barcodescanning]
comments: true
share: true
---

With the advancement in technology, barcode scanning has become an essential feature in many mobile applications. In Flutter, we can leverage the `MediaQuery` class to implement a responsive barcode scanning experience across different devices. Let's dive into the implementation details.

## Prerequisites

To follow along with this tutorial, make sure you have Flutter installed on your machine. You can check the installation guide on the [official Flutter website](https://flutter.dev/docs/get-started/install).

## Step 1: Add Dependencies

First, we need to add the necessary dependencies to our Flutter project. Open the `pubspec.yaml` file and add the following lines under the `dependencies` section:

```yaml
dependencies:
  barcode_scan: ^2.0.0
  qr_code_scanner: ^0.4.0
```

Save the file and run `flutter pub get` in the terminal to fetch the packages.

## Step 2: Configure Permissions

Next, we need to configure the necessary permissions to access the camera for barcode scanning. Open the `AndroidManifest.xml` file located under the `android/app/src/main` directory and add the following line:

```xml
<uses-permission android:name="android.permission.CAMERA" />
```

For iOS, open the `Info.plist` file located under the `ios/Runner` directory and add the following lines:

```xml
<key>NSCameraUsageDescription</key>
<string>Allow access to the camera for barcode scanning</string>
```

Make sure to replace the permission description with an appropriate message for your app.

## Step 3: Implement Barcode Scanning Widget

Now we can start implementing the barcode scanning widget in our Flutter app. Create a new file named `barcode_scanner.dart`, and add the following code:

```dart
import 'package:barcode_scan/barcode_scan.dart';
import 'package:flutter/material.dart';
import 'package:qr_code_scanner/qr_code_scanner.dart';

class BarcodeScanner extends StatefulWidget {
  @override
  _BarcodeScannerState createState() => _BarcodeScannerState();
}

class _BarcodeScannerState extends State<BarcodeScanner> {
  final GlobalKey qrKey = GlobalKey(debugLabel: 'QR');
  QRViewController? _controller;
  bool _scanned = false;
  
  @override
  void dispose() {
    _controller?.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return MediaQuery(
      data: MediaQuery.of(context).copyWith(padding: EdgeInsets.zero),
      child: Scaffold(
        body: _buildScannerView(),
      ),
    );
  }

  Widget _buildScannerView() {
    return QRView(
      key: qrKey,
      onQRViewCreated: _onQRViewCreated,
    );
  }

  void _onQRViewCreated(QRViewController controller) {
    setState(() {
      _controller = controller;
    });
    _controller!.scannedDataStream.listen((barcode) {
      if (!_scanned) {
        _scanned = true;
        // Handle the scanned barcode here
        print(barcode);
      }
    });
  }
}
```

## Step 4: Implement Usage of BarcodeScanner Widget

Now, let's implement the usage of the `BarcodeScanner` widget in our app. Open the main entry point file (`main.dart` by default) and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'barcode_scanner.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Barcode Scanner Demo',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: Scaffold(
        appBar: AppBar(
          title: Text('Barcode Scanner Demo'),
        ),
        body: Center(
          child: ElevatedButton(
            child: Text('Scan Barcode'),
            onPressed: () {
              Navigator.push(
                context,
                MaterialPageRoute(builder: (context) => BarcodeScanner()),
              );
            },
          ),
        ),
      ),
    );
  }
}
```

Save the file and run the app using `flutter run` command in the terminal. You should see a button labeled "Scan Barcode" in the app, and upon clicking it, the barcode scanner view will be displayed.

That's it! You have now implemented responsive barcode scanning using `MediaQuery` in Flutter. You can further extend this implementation by adding barcode scanning functionality to your specific use case.

#flutter #barcodescanning