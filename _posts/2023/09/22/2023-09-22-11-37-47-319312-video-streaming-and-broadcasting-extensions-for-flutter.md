---
layout: post
title: "Video streaming and broadcasting extensions for Flutter"
description: " "
date: 2023-09-22
tags: [AgoraFlutterSDK), DailycoFlutterSDK)]
comments: true
share: true
---

Flutter is a popular open-source framework for creating cross-platform mobile applications. With its rich set of libraries and plugins, Flutter enables developers to build high-performance and feature-rich apps. If you're looking to add video streaming and broadcasting capabilities to your Flutter app, there are several excellent extensions available that can help you achieve just that. In this article, we will explore some of these extensions and their key features.

## 1. Agora Flutter SDK (#AgoraFlutterSDK)

![Agora Flutter SDK](https://www.example.com/agora_flutter_sdk.png)

One of the most widely used video streaming and broadcasting extensions for Flutter is the Agora Flutter SDK. Agora.io provides developers with a comprehensive set of tools and APIs to integrate real-time audio, video, and interactive broadcasting capabilities into their applications.

**Key Features:**
- Real-time video and audio communication
- High-quality video streaming with adaptive bitrate technology
- Support for multi-channel and multi-host broadcasting
- Interactive broadcasting with features like screen sharing and whiteboard
- Cross-platform compatibility (iOS, Android, Web)

**Example Code:**
```dart
import 'package:agora_rtc_engine/rtc_engine.dart';

void initAgora() {
  RtcEngine.create('<YOUR_APP_ID>');
  // Initialize Agora SDK and configure settings
}

void joinChannel(String channelName) {
  RtcEngine.joinChannel('<YOUR_TOKEN>', channelName, null, 0);
  // Join a specific channel for communication or broadcasting
}

void leaveChannel() {
  RtcEngine.leaveChannel();
  // Leave the current channel
}

void disposeAgora() {
  RtcEngine.destroy();
  // Release resources and destroy the Agora SDK instance
}
```

## 2. Daily.co Flutter SDK (#DailycoFlutterSDK)

![Daily.co Flutter SDK](https://www.example.com/dailyco_flutter_sdk.png)

Another popular option for video streaming and broadcasting in Flutter is the Daily.co Flutter SDK. Daily.co provides developers with a simple and reliable platform for building real-time video and audio applications.

**Key Features:**
- Low-latency video streaming
- Customizable video conferencing UI components
- Multi-party video calls with up to 50 participants
- Screen sharing and recording capabilities
- Cross-platform compatibility (iOS, Android, Web)

**Example Code:**
```dart
import 'package:daily_co/daily_co.dart';

void createCall(String callUrl) {
  DailyCo.call(callUrl);
  // Create a video call using the specified call URL
}

void joinCall(String callUrl) {
  DailyCo.call(callUrl);
  // Join an existing video call using the specified call URL
}

void leaveCall() {
  DailyCo.hangUp();
  // Leave the current video call
}

void toggleMic(bool enabled) {
  DailyCo.setLocalAudio(enabled);
  // Enable or disable the local microphone during a call
}

void toggleCamera(bool enabled) {
  DailyCo.setLocalVideo(enabled);
  // Enable or disable the local camera during a call
}
```

## Conclusion

These are just two of the many video streaming and broadcasting extensions available for Flutter. Whether you're building a video conferencing app, a live streaming platform, or any other application that requires real-time video communication, these extensions can provide you with the necessary tools and APIs to integrate those functionalities seamlessly. Choose the one that best fits your project requirements and start building amazing video applications with Flutter today!