---
layout: post
title: "How to write platform-specific code in Flutter?"
description: " "
date: 2023-09-18
tags: [import, import]
comments: true
share: true
---

Flutter is a popular framework for building cross-platform mobile applications. However, sometimes you may need to write platform-specific code to access features that are unique to a particular platform, such as accessing the device's camera or sending push notifications. In this blog post, we will explore how to write platform-specific code in Flutter using the platform channels.

## What are platform channels?

Platform channels are a mechanism provided by Flutter to communicate between the Dart code and the native code of the underlying platform (Android or iOS). This allows you to write platform-specific code using the native languages, such as Java/Kotlin for Android and Objective-C/Swift for iOS, and integrate it seamlessly with your Flutter app.

## Step 1: Create platform-specific methods

The first step is to define the platform-specific methods in your Flutter app. These methods will act as a bridge between the Dart code and the native code. To do this, you need to create a platform interface using the `MethodChannel` class provided by Flutter.

```dart
import 'package:flutter/services.dart';

class PlatformUtils {
  static const MethodChannel _channel =
      MethodChannel('com.example.app/platform_utils');

  static Future<String> getPlatformVersion() async {
    try {
      final String version =
          await _channel.invokeMethod('getPlatformVersion');
      return version;
    } catch (e) {
      throw Exception('Failed to get platform version.');
    }
  }
}
```

In the above code, we define a `getPlatformVersion` method that can be called from the Dart code to retrieve the platform version. The `MethodChannel` is initialized with a unique channel name that should match the channel name used in the native code.

## Step 2: Implement platform-specific code

Next, you need to implement the platform-specific code in the native languages. In this example, we will show the implementation for Android, but similar steps can be followed for iOS.

### Android (Java)

Create a new Java class that extends `FlutterActivity`, and register the method channel used in the Flutter code.

```java
import io.flutter.embedding.android.FlutterActivity;
import io.flutter.embedding.engine.FlutterEngine;
import io.flutter.plugin.common.MethodChannel;

public class MainActivity extends FlutterActivity {
    private static final String CHANNEL = "com.example.app/platform_utils";

    @Override
    public void configureFlutterEngine(FlutterEngine flutterEngine) {
        super.configureFlutterEngine(flutterEngine);
        new MethodChannel(flutterEngine.getDartExecutor().getBinaryMessenger(), CHANNEL)
                .setMethodCallHandler((call, result) -> {
                    if (call.method.equals("getPlatformVersion")) {
                        result.success(android.os.Build.VERSION.RELEASE);
                    } else {
                        result.notImplemented();
                    }
                });
    }
}
```

In the above code, we register the `getPlatformVersion` method and retrieve the Android version from the system. Any other platform-specific code can be written and registered similarly.

### iOS (Objective-C)

Create a new Objective-C class and import the `Flutter/Flutter.h` framework. Register the method channel similarly to Android.

```objective-c
#import "AppDelegate.h"
#import "GeneratedPluginRegistrant.h"

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    FlutterViewController *flutterViewController = (FlutterViewController *)self.window.rootViewController;
    
    FlutterMethodChannel *channel =
        [FlutterMethodChannel methodChannelWithName:@"com.example.app/platform_utils"
                                    binaryMessenger:flutterViewController.binaryMessenger];
    [channel setMethodCallHandler:^(FlutterMethodCall *call, FlutterResult result) {
        if ([call.method isEqualToString:@"getPlatformVersion"]) {
            result([UIDevice currentDevice].systemVersion);
        } else {
            result(FlutterMethodNotImplemented);
        }
    }];
    
    [GeneratedPluginRegistrant registerWithRegistry:self];
    return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

@end
```

## Step 3: Use platform-specific code in Flutter

Finally, you can use the platform-specific code in your Flutter app by calling the methods defined in the Dart code.

```dart
String platformVersion = await PlatformUtils.getPlatformVersion();
print('Platform version: $platformVersion');
```

In this example, we call the `getPlatformVersion` method and retrieve the platform version using the platform channel. You can now use this information to provide platform-specific behavior in your Flutter app.

## Conclusion

Writing platform-specific code in Flutter allows you to access native features and capabilities of each platform. By leveraging platform channels, you can bridge the gap between the Dart code and the native code, enabling seamless integration of platform-specific code in your Flutter app.