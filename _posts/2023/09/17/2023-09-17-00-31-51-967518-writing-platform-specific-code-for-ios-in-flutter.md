---
layout: post
title: "Writing platform-specific code for iOS in Flutter."
description: " "
date: 2023-09-17
tags: [import, include, include, platformchannels, flutterdevelopment]
comments: true
share: true
---

Flutter is a powerful cross-platform framework that allows developers to write apps using a single codebase for both iOS and Android. However, there may be instances where you need to write platform-specific code to achieve certain functionalities or take advantage of iOS-specific features. In this blog post, we will explore how to write platform-specific code for iOS in Flutter.

## Platform Channels

Flutter provides a mechanism called [platform channels](https://flutter.dev/docs/development/platform-integration/platform-channels) that allows communication between Flutter and the underlying platform, in this case, iOS. With platform channels, you can invoke native code methods and receive callbacks in your Flutter app.

To start, you need to define a method channel in your Flutter code, specifying the channel name and the platform-specific code identifier. Here's an example:

```dart
import 'package:flutter/services.dart';

const platform = MethodChannel('my_channel');

// Invoking iOS-specific method
String getiOSVersion() {
  try {
    return await platform.invokeMethod('getiOSVersion');
  } on PlatformException catch (e) {
    return 'Error: ${e.message}';
  }
}
```

In this example, we define a method channel named `my_channel`. We then create a method called `getiOSVersion()` that invokes the 'getiOSVersion' method on the iOS side. The `invokeMethod` function returns a Future, allowing us to await the result.

## Writing Platform-Specific Code in iOS

To implement the platform-specific code in iOS, you need to navigate to the `AppDelegate.m` file in your iOS project. Inside the `AppDelegate` class, you can add the necessary method that will be called from the Flutter app. Here's an example of adding a method to retrieve the iOS version:

```objective-c
#import "AppDelegate.h"

@implementation AppDelegate

// ...

- (NSString *)getiOSVersion {
    return [[UIDevice currentDevice] systemVersion];
}

@end
```

In this example, we add the `getiOSVersion` method to the `AppDelegate` class, which returns the iOS version using `[[UIDevice currentDevice] systemVersion]`.

## Registering the Method Channel in iOS

Finally, you need to register the method channel in the iOS project. Inside the `didFinishLaunchingWithOptions` method in your `AppDelegate.m` file, add the following code:

```objective-c
#include "AppDelegate.h"
#include "GeneratedPluginRegistrant.h"

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application
    didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  // ...

  FlutterViewController* flutterViewController = (FlutterViewController*)self.window.rootViewController;
  FlutterMethodChannel* channel = [FlutterMethodChannel
      methodChannelWithName:@"my_channel"
            binaryMessenger:flutterViewController];
  [channel setMethodCallHandler:^(FlutterMethodCall* call, FlutterResult result) {
    if ([@"getiOSVersion" isEqualToString:call.method]) {
      NSString* iOSVersion = [self getiOSVersion];
      result(iOSVersion);
    } else {
      result(FlutterMethodNotImplemented);
    }
  }];

  // ...

  return [super application:application didFinishLaunchingWithOptions:launchOptions];
}

// ...

@end
```

In this code snippet, we register the method channel using the `initWithName` method, passing the channel name defined in Flutter and the `flutterViewController` as the binary messenger.

## Conclusion

Writing platform-specific code for iOS in Flutter is made possible by using platform channels. By leveraging the power of platform channels, you can access iOS-specific features and functionalities within your Flutter app. Remember to test your code thoroughly to ensure it performs as expected on the iOS platform.

#flutter #ios #platformchannels #flutterdevelopment