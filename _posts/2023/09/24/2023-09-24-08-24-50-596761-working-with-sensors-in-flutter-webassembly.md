---
layout: post
title: "Working with sensors in Flutter WebAssembly"
description: " "
date: 2023-09-24
tags: [FlutterWeb, SensorIntegration]
comments: true
share: true
---

Flutter, Google's UI toolkit for building natively compiled applications, has gained popularity for developing cross-platform mobile applications. With the advent of Flutter WebAssembly (WASM), developers can now leverage the power of Flutter to create web applications as well.

However, working with sensors in Flutter WebAssembly requires a different approach compared to traditional mobile app development. In this blog post, we'll explore how to work with sensors in Flutter WASM and demonstrate a simple example using the device orientation sensor.

## Setting up the Project

Before we begin, make sure you have Flutter SDK installed on your machine. If not, you can follow the official Flutter documentation to set it up.

Once you have Flutter installed, create a new Flutter project using the following command:

```
$ flutter create flutter_wasm_sensors_example
```

Change into the project directory:

```
$ cd flutter_wasm_sensor_example
```

Open the project in your preferred IDE or editor.

## Adding the Sensor Package

Flutter WebAssembly does not have built-in support for accessing device sensors like the accelerometer or gyroscope. However, you can use third-party packages to achieve this. One popular package is the `sensors` package.

To add the `sensors` package to your project, open the `pubspec.yaml` file and add the following line under the `dependencies` section:

```yaml
dependencies:
  sensors: ^0.4.4
```

Save the file and run the following command to download and update the package:

```
$ flutter packages get
```

## Accessing the Device Orientation

To demonstrate working with sensors, let's access the device orientation sensor and display its values on the screen.

First, create a new file called `sensor_screen.dart` in the `lib` directory of your project. In this file, add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:sensors/sensors.dart';

class SensorScreen extends StatefulWidget {
  @override
  _SensorScreenState createState() => _SensorScreenState();
}

class _SensorScreenState extends State<SensorScreen> {
  String _orientation = '';

  @override
  void initState() {
    super.initState();
    accelerometerEvents.listen((event) {
      setState(() {
        _orientation = event.toString();
      });
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Device Orientation Sensor'),
      ),
      body: Center(
        child: Text(
          _orientation,
          style: TextStyle(fontSize: 24),
        ),
      ),
    );
  }
}
```

In this code, we define a `SensorScreen` widget that extends `StatefulWidget`. We initialize a string `_orientation` to store the device orientation values.

In the `initState` method, we listen to the `accelerometerEvents` stream provided by the `sensors` package. Whenever a new event is emitted, we update the `_orientation` variable and trigger a rebuild of the UI.

Finally, in the `build` method, we display the current orientation value on the screen.

## Adding the Sensor Screen

To test the sensor integration, let's add the `SensorScreen` widget to the application in the `main.dart` file.

Replace the contents of `lib/main.dart` with the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_wasm_sensors_example/sensor_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter WASM Sensors Example',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: SensorScreen(),
    );
  }
}
```

Now, save the file and run the application using the following command:

```
$ flutter run -d chrome
```

If everything goes well, the application will open in your web browser, and you should see the "Device Orientation Sensor" title at the top, with the current sensor values displayed in the center of the screen.

## Conclusion

In this blog post, we learned how to work with sensors in Flutter WebAssembly. We explored how to add the `sensors` package, access the device orientation sensor, and display the sensor values on the screen.

Remember that accessing sensors in Flutter WebAssembly requires the use of third-party packages, as the platform doesn't provide native support. Always refer to the package documentation for more advanced sensor integration.

Happy coding! #FlutterWeb #SensorIntegration