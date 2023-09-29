---
layout: post
title: "Working with AR objects and animations using GetX"
description: " "
date: 2023-09-29
tags: [GetX, AugmentedReality, Flutter]
comments: true
share: true
---

AR (Augmented Reality) is an exciting technology that allows us to merge virtual objects with the real world. With the help of GetX, a state management library in Flutter, we can create immersive AR experiences with ease. In this article, we will explore how to work with AR objects and animations using GetX.

## Setting up dependencies

To get started, we need to add the necessary dependencies to our Flutter project. Open your `pubspec.yaml` file and add the following lines:

```yaml
dependencies:
  arcore_flutter_plugin: ^<latest_version>
  arkit_flutter_plugin: ^<latest_version>
  get: ^<latest_version>
```

Replace `<latest_version>` with the current versions of `arcore_flutter_plugin`, `arkit_flutter_plugin`, and `get`.

## Creating an AR scene

First, let's create an AR scene using ARCore or ARKit, based on the platform you are targeting. 

For ARCore (Android), create a new `ARCoreView` widget:

```dart
import 'package:arcore_flutter_plugin/arcore_flutter_plugin.dart';

class ARScene extends StatelessWidget {
  final ARCoreController arController = ARCoreController();

  @override
  Widget build(BuildContext context) {
    return ARCoreView(
      onARCoreViewCreated: arController.onARCoreViewCreated,
    );
  }
}
```

For ARKit (iOS), create a new `ARKitView` widget:

```dart
import 'package:arkit_plugin/arkit_plugin.dart';

class ARScene extends StatelessWidget {
  final ARKitController arController = ARKitController();

  @override
  Widget build(BuildContext context) {
    return ARKitView(
      onARKitViewCreated: arController.onARKitViewCreated,
    );
  }
}
```

## Adding AR objects and animations

Now, let's add AR objects and animations to our scene. We will use GetX to manage the state and control the animations.

First, create a GetX controller to manage the AR scene and animations:

```dart
import 'package:get/get.dart';

class ARController extends GetxController {
  final _isAnimating = false.obs;
  bool get isAnimating => _isAnimating.value;

  void startAnimation() {
    _isAnimating.value = true;
    // Perform animation logic here
  }

  void stopAnimation() {
    _isAnimating.value = false;
    // Perform stop animation logic here
  }
}
```

Next, update your `ARScene` widget to use the `ARController`:

```dart
class ARScene extends StatelessWidget {
  final ARController arController = Get.put(ARController());

  // Widget build method remains the same

  Widget build(BuildContext context) {
    // ...
  }
}
```

To start and stop the animations, you can use the following methods:

```dart
FloatingActionButton(
  onPressed: () {
    if (arController.isAnimating) {
      arController.stopAnimation();
    } else {
      arController.startAnimation();
    }
  },
  child: Icon(Icons.play_arrow),
),
```

Finally, add your AR objects and animations inside the `onARCoreViewCreated` or `onARKitViewCreated` callbacks. These callbacks allow you to access the AR scene and perform AR-related operations.

## Conclusion

In this article, we explored how to work with AR objects and animations using GetX in Flutter. We set up the necessary dependencies, created an AR scene, added AR objects, and controlled animations using GetX. With GetX's powerful state management capabilities, we can create interactive and immersive AR experiences effortlessly. Happy coding!

#AR #GetX #AugmentedReality #Flutter