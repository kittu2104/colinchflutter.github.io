---
layout: post
title: "How to listen for device pixel ratio changes using MediaQuery in Flutter?"
description: " "
date: 2023-10-01
tags: [Flutter, MediaQuery, Flutter, MediaQuery]
comments: true
share: true
---
title: How to Listen for Device Pixel Ratio Changes using MediaQuery in Flutter
date: 2021-09-10
tags: #Flutter #MediaQuery

---

In Flutter, the MediaQuery class provides a way to access information about the user's device, such as the screen size, orientation, and pixel density. However, there are cases where you may want to be notified whenever the device's pixel ratio changes dynamically. This can be useful when you need to adjust your UI based on the pixel density of the device.

To listen for device pixel ratio changes using MediaQuery in Flutter, you can make use of the `addListener` method. Here's how you can do it:

```dart
import 'package:flutter/material.dart';

class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  double devicePixelRatio = 1.0;

  @override
  void initState() {
    super.initState();
    MediaQuery.of(context).addListener(updateDevicePixelRatio);
  }

  @override
  void dispose() {
    MediaQuery.of(context).removeListener(updateDevicePixelRatio);
    super.dispose();
  }

  void updateDevicePixelRatio() {
    setState(() {
      devicePixelRatio = MediaQuery.of(context).devicePixelRatio;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Device Pixel Ratio'),
      ),
      body: Center(
        child: Text(
          'Device Pixel Ratio: $devicePixelRatio',
          style: TextStyle(fontSize: 24.0),
        ),
      ),
    );
  }
}
```

In the above example, we have a StatefulWidget called `MyWidget`. In the `initState` method, we add a listener to the MediaQuery using `addListener` and provide the `updateDevicePixelRatio` callback function. In the `updateDevicePixelRatio` function, we update the `devicePixelRatio` property of the state by accessing `MediaQuery.of(context).devicePixelRatio`. 

Remember to remove the listener in the `dispose` method to avoid memory leaks.

Now you can use the `devicePixelRatio` property in your UI to make adjustments based on the device's pixel density.

By following the steps above, you can easily listen for device pixel ratio changes using MediaQuery in Flutter. This can help you create responsive UIs that adapt to different screen densities and provide a better user experience.

#Flutter #MediaQuery