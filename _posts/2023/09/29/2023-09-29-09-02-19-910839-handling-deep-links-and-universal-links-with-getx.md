---
layout: post
title: "Handling deep links and universal links with GetX"
description: " "
date: 2023-09-29
tags: [Flutter, GetX]
comments: true
share: true
---

## Deep Links
A deep link is a URL that points to a specific location within your app. For example, `myapp://products/123` could be a deep link that opens a product detail page with the ID 123.

To handle deep links in Flutter, we can utilize the `flutter_deeplink` package along with GetX to make the integration easier. 

First, add the following dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_deeplink: ^0.5.1
  get: ^4.1.4
  // other dependencies
```

Next, create a new file called `deeplinks.dart` and import the necessary packages:

```dart
import 'package:get/get.dart';
import 'package:flutter_deeplink/flutter_deeplink.dart';
```

Inside the `deeplinks.dart` file, set up a method to handle the deep link:

```dart
void handleDeepLink() {
  Get.put(DeepLinkRouter(), permanent: true);
  final router = Get.find<DeepLinkRouter>();

  FlutterDeepLink(
    router: router,
  ).init();
}
```

Here, we use GetX's `Get.put()` method to register an instance of the `DeepLinkRouter` class as a permanent dependency. The `DeepLinkRouter` class will handle the routing based on the deep link path.

Next, create the `DeepLinkRouter` class:

```dart
class DeepLinkRouter extends Router {
  @override
  void defineRoute(FlutterDeepLinkRouter router) {
    router.addRoute(
      path: '/products/:id',
      builder: (route, params, queryParams) => ProductDetailPage(productId: params['id'] as String),
    );
  }
}
```

In the above code snippet, we define a route for the `/products/:id` deep link path. When this deep link is triggered, it will navigate to the `ProductDetailPage`, passing the `productId` as a parameter.

Don't forget to register the `handleDeepLink()` method in your Flutter app's `main.dart` file:

```dart
void main() {
  runApp(MyApp());
  
  WidgetsBinding.instance.addPostFrameCallback((_) {
    handleDeepLink();
  });
}
```

Now, whenever a deep link with the specified path is triggered, the corresponding page will be opened within your Flutter app.

## Universal Links
Universal links are similar to deep links, but they are associated with a website and allow users to open your app directly from a web page. To handle universal links in your Flutter app with GetX, you need to configure your iOS and Android projects correctly.

For iOS, you need to set up the `Associated Domains` capability in the `Signing & Capabilities` tab of your Xcode project. Add your app's domain in the following format: `applinks:yourappdomain.com`. Then, follow the necessary steps to verify and publish your domain.

For Android, you need to configure the `AndroidManifest.xml` file. Add the following intent filters to your app's default activity within the `<activity>` tag:

```xml
<intent-filter>
  <action android:name="android.intent.action.VIEW" />
  <category android:name="android.intent.category.DEFAULT" />
  <category android:name="android.intent.category.BROWSABLE" />

  <!-- Add your app link host and scheme -->
  <data android:host="yourappdomain.com" android:scheme="http"/>
  <data android:host="yourappdomain.com" android:scheme="https"/>
</intent-filter>
```

Once the configurations are in place, you can handle universal links similar to deep links by following the previous steps.

Handling deep links and universal links is essential for a seamless user experience and easy content navigation within your app. The GetX package, along with the `flutter_deeplink` package, makes it straightforward to implement deep and universal linking in your Flutter applications. Start integrating these features into your app to enhance user engagement and improve accessibility to specific content within your app.

#Flutter #GetX