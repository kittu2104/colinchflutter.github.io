---
layout: post
title: "Implementing audio streaming from remote servers with Flutter Sound"
description: " "
date: 2023-09-28
tags: [audio, streaming]
comments: true
share: true
---

Flutter Sound is a powerful audio plugin for Flutter that provides support for audio recording and playback. In addition to these core features, Flutter Sound can also be used to stream audio from remote servers. In this blog post, we will explore how to implement audio streaming from remote servers using Flutter Sound.

## Prerequisites

Before we begin, ensure that you have Flutter and Flutter Sound installed and set up in your development environment. You can follow the official documentation to install Flutter ([https://flutter.dev](https://flutter.dev)) and Flutter Sound ([https://pub.dev/packages/flutter_sound](https://pub.dev/packages/flutter_sound)).

## Fetching audio data from a remote server

To stream audio from a remote server, you first need to fetch the audio data from the server. You can use any preferred method to fetch the audio data, such as making an HTTP GET request or using a third-party library like Dio or http.

Here's an example using the http library to fetch audio data from a remote server:

```dart
import 'dart:io';
import 'package:http/http.dart' as http;

Future<List<int>> fetchAudioData(String url) async {
  final response = await http.get(Uri.parse(url));
  if (response.statusCode != 200) {
    throw HttpException('Failed to fetch audio data');
  }
  return response.bodyBytes;
}
```

## Playing audio with Flutter Sound

Once you have fetched the audio data, you can use Flutter Sound's playback functionality to play the audio.

Here's an example of how to play the fetched audio data using Flutter Sound:

```dart
import 'package:flutter_sound/flutter_sound.dart';

FlutterSoundPlayer _soundPlayer = FlutterSoundPlayer();

void playAudio(List<int> audioData) async {
  await _soundPlayer.openAudioSession();
  await _soundPlayer.startPlayerFromStream(
    codec: Codec.defaultCodec,
    numChannels: 2,
    sampleRate: 44100,
    bitRate: 128000,
    androidAudioSource: AndroidAudioSource.MIC,
    iosAudioSource: IosAudioSource.MIC,
    stream: audioData,
  );
}

void stopAudio() async {
  await _soundPlayer.stopPlayer();
  await _soundPlayer.closeAudioSession();
}
```

In the `playAudio` function, we open the audio session, specify the audio codec, channels, sample rate, bit rate, and audio source. We then start the player by passing in the fetched audio data as a stream.

The `stopAudio` function is used to stop the audio playback and close the audio session.

## Conclusion

In this blog post, we have seen how to implement audio streaming from remote servers using Flutter Sound. By combining the ability to fetch audio data from a remote server with Flutter Sound's playback functionality, you can create powerful audio streaming applications with Flutter.

#flutter #audio #streaming