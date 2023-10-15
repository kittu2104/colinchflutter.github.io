---
layout: post
title: "Popular Flutter plugins for ads integration"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

When it comes to monetizing your Flutter app, integrating ads is a popular choice. Luckily, there are several great plugins available that make it easy to incorporate ads into your app. In this article, we will explore some of the most popular Flutter plugins for ads integration.

## 1. Google Mobile Ads (AdMob)

The **Google Mobile Ads** plugin, also known as **AdMob**, is a widely used plugin for integrating ads in Flutter apps. AdMob is Google's advertising platform that allows you to display both banner and interstitial ads.

To use Google Mobile Ads in your Flutter app, you need to add the `firebase_admob` dependency to your `pubspec.yaml` file. You can then follow the official documentation to implement banner and interstitial ads in your app.

Here is an example of how you can show a banner ad using the AdMob plugin:

```dart
import 'package:firebase_admob/firebase_admob.dart';

void main() {
  FirebaseAdMob.instance.initialize(appId: 'YOUR_ADMOB_APP_ID');
  BannerAd bannerAd = BannerAd(
    adUnitId: 'YOUR_BANNER_AD_UNIT_ID',
    size: AdSize.banner,
    targetingInfo: MobileAdTargetingInfo(),
    listener: (MobileAdEvent event) {
      print("BannerAd event is $event");
    },
  );
  bannerAd
    ..load()
    ..show();
}
```

Make sure to replace `YOUR_ADMOB_APP_ID` and `YOUR_BANNER_AD_UNIT_ID` with your own AdMob app ID and ad unit ID.

## 2. Facebook Audience Network (FAN)

The **Facebook Audience Network** plugin (known as **FAN**) is another popular choice for integrating ads in Flutter apps. FAN provides access to Facebook's advertising platform, which includes a wide range of ad formats such as banners, interstitials, and rewarded videos.

To use Facebook Audience Network in your Flutter app, you need to add the `flutter_facebook_audience_network` dependency to your `pubspec.yaml` file. You can then follow the official documentation to implement different ad formats in your app.

Here is an example of how you can show a banner ad using the Facebook Audience Network plugin:

```dart
import 'package:flutter_facebook_audience_network/flutter_facebook_audience_network.dart';

void main() {
  FacebookAudienceNetwork.init(
    testingId: 'YOUR_TESTING_DEVICE_ID',
  );
  final size = MediaQuery.of(context).size;
  FacebookBannerAd(
    placementId: 'YOUR_BANNER_PLACEMENT_ID',
    bannerSize: BannerSize.STANDARD,
    listener: (result, value) {
      print("BannerAd event is $result -> $value");
    },
  );
}
```

Make sure to replace `YOUR_TESTING_DEVICE_ID` and `YOUR_BANNER_PLACEMENT_ID` with your own testing device ID and banner placement ID.

## Conclusion

Integrating ads into your Flutter app can be made easier with the help of popular plugins like Google Mobile Ads (AdMob) and Facebook Audience Network (FAN). These plugins provide a wide range of ad formats and comprehensive documentation, making it simple for developers to monetize their apps through ads.

Remember to choose the plugin that best fits your needs and ensure that you comply with the respective advertising platforms' policies and guidelines.