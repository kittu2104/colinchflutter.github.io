---
layout: post
title: "Implementing audio stream caching and offline playback in Flutter"
description: " "
date: 2023-09-18
tags: [audio]
comments: true
share: true
---

With Flutter's rich set of libraries and plugins, it's possible to implement audio stream caching and offline playback seamlessly. In this blog post, we will explore how to achieve this using Flutter.

## Why Do We Need Audio Stream Caching?

Streaming audio content directly from the internet consumes data and requires a stable network connection. Implementing audio stream caching can improve the user experience by providing offline playback capabilities and reducing data usage.

## Implementing Audio Stream Caching

To implement audio stream caching in Flutter, we can make use of the `dio` library for network requests and the `flutter_cache_manager` library for caching.

First, add the following dependencies to your `pubspec.yaml` file:

```
dependencies:
  dio: ^4.0.0
  flutter_cache_manager: ^3.2.0
```
Don't forget to run `flutter pub get` to fetch the dependencies.

Next, let's define a class for our audio cache manager:

```dart
import 'package:flutter_cache_manager/flutter_cache_manager.dart';

class AudioCacheManager extends BaseCacheManager {
  static const key = 'audio_cache';

  static AudioCacheManager? _instance;

  factory AudioCacheManager() {
    if (_instance == null) {
      _instance = AudioCacheManager._();
    }
    return _instance!;
  }

  AudioCacheManager._() : super(key);
}
```
This class extends the `BaseCacheManager` provided by `flutter_cache_manager`. By overriding the `getSingleFile` method, we can intercept and cache audio files when they are requested.

Now, let's create a function to fetch and cache the audio stream:

```dart
import 'package:dio/dio.dart';
import 'package:flutter_cache_manager/flutter_cache_manager.dart';

Future<String> cacheAudioStream(String url) async {
  final cacheManager = AudioCacheManager();
  final fileInfo = await cacheManager.downloadFile(url);

  if (fileInfo != null && fileInfo.statusCode == 200) {
    return fileInfo.file.path;
  } else {
    throw Exception('Failed to cache audio stream!');
  }
}
```

In this function, we create an instance of our `AudioCacheManager` and use the `downloadFile` method to download and cache the audio stream. If the download is successful, we return the path of the cached file. Otherwise, we throw an exception.

## Offline Playback

To enable offline playback, we can utilize Flutter's `flutter_audio_service` library. First, add the following dependencies to your `pubspec.yaml` file:

```
dependencies:
  flutter_audio_service: ^0.16.2
  just_audio: ^0.12.1
```
Again, run `flutter pub get` to fetch the dependencies.

Next, create a media task handler to handle audio playback:

```dart
import 'package:just_audio/just_audio.dart';
import 'package:flutter_audio_service/flutter_audio_service.dart';

class AudioPlayerTask extends BackgroundAudioTask {
  final _audioPlayer = AudioPlayer();

  @override
  Future<void> onStart(Map<String, dynamic>? params) async {
    final url = params!['url'] as String;
    await _audioPlayer.setUrl(url);
    _audioPlayer.play();
  }

  @override
  Future<void> onStop() async {
    await _audioPlayer.stop();
  }
}
```

Here, we define a task handler that extends `BackgroundAudioTask` provided by `flutter_audio_service`. In the `onStart` method, we retrieve the audio stream URL from the parameters and use the `just_audio` library to start playing the audio. The `onStop` method is called when playback is stopped.

To start playback, we can use the following code:

```dart
FlutterAudioService.start(
  backgroundTaskEntrypoint: AudioPlayerTask.start,
  androidNotificationChannelName: 'Audio playback',
  androidNotificationColor: 0xFF2196f3,
  androidNotificationIcon: 'mipmap/ic_launcher',
  androidEnableQueue: true,
);
```

In this code snippet, we use the `FlutterAudioService.start` method to start playing audio in the background. We specify the entry point using the `AudioPlayerTask.start` method. Additionally, we can customize the Android notification by providing the channel name, color, and icon.

## Conclusion

By implementing audio stream caching and offline playback in Flutter, we can enhance the user experience and reduce data usage. Utilizing the `dio` and `flutter_cache_manager` libraries for caching and the `flutter_audio_service` and `just_audio` libraries for offline playback ensures a seamless audio streaming experience in your Flutter app.

#flutter #audio #streaming #caching