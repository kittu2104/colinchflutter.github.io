---
layout: post
title: "Using GetX for audio and video playback in Flutter"
description: " "
date: 2023-09-29
tags: [GetX, multimedia, audioPlayback, videoPlayback]
comments: true
share: true
---

With the growing demand for multimedia applications, it has become essential for developers to incorporate audio and video playback features in their Flutter apps. GetX, a powerful state management library, can come in handy for implementing these functionalities with ease. In this blog post, we will explore how to use GetX for audio and video playback in Flutter.

## Installing GetX

Before we delve into integrating audio and video playback, we need to install the Get library in our Flutter project. Simply add the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  get: ^4.1.4
```

## Audio Playback with GetX

To play audio files with GetX, we can leverage the `audioplayers` package, which is compatible with GetX. First, we need to add the `audioplayers` dependency to our `pubspec.yaml` file:

```yaml
dependencies:
  get: ^4.1.4
  audioplayers: ^0.21.1
```

Next, let's define a controller for audio playback using GetX. Create a new file called `audio_controller.dart` and add the following code:

```dart
import 'package:get/get.dart';
import 'package:audioplayers/audioplayers.dart';

class AudioController extends GetxController {
  AudioPlayer? audioPlayer;

  Future<void> playAudio(String url) async {
    audioPlayer = AudioPlayer();
    await audioPlayer!.play(url);
  }

  Future<void> stopAudio() async {
    await audioPlayer!.stop();
    audioPlayer!.dispose();
  }
}
```

In this code, we create an `AudioPlayer` instance and define two methods: `playAudio` and `stopAudio`. The `playAudio` method takes a URL as input and starts playing the audio using the `AudioPlayer`. The `stopAudio` method stops the audio playback and disposes of the `AudioPlayer`.

Now, let's create a UI for audio playback. In your main screen, add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

import 'audio_controller.dart';

class AudioScreen extends StatelessWidget {
  final audioController = Get.put(AudioController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Audio Player'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: () {
                audioController.playAudio('YOUR_AUDIO_URL');
              },
              child: Text('Play Audio'),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                audioController.stopAudio();
              },
              child: Text('Stop Audio'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In this code, we instantiate the `AudioController` using `Get.put` in the `audioController` variable. Then, we create a simple UI with two buttons to play and stop the audio. Modify the `'YOUR_AUDIO_URL'` with the actual URL of the audio file you want to play.

## Video Playback with GetX

Now, let's move on to video playback using GetX. For this, we can use the `chewie` package along with GetX. Begin by adding the `chewie` and `video_player` dependencies to your `pubspec.yaml` file:

```yaml
dependencies:
  get: ^4.1.4
  chewie: ^1.2.2
  video_player: ^2.1.6
```

Next, create a new file called `video_controller.dart` and add the following code:

```dart
import 'package:get/get.dart';
import 'package:chewie/chewie.dart';
import 'package:video_player/video_player.dart';

class VideoController extends GetxController {
  VideoPlayerController? videoPlayerController;
  ChewieController? chewieController;

  Future<void> initializeVideo(String url) async {
    videoPlayerController = VideoPlayerController.network(url);
    await videoPlayerController!.initialize();
    chewieController = ChewieController(
      videoPlayerController: videoPlayerController!,
      autoPlay: false,
      looping: false,
    );
  }

  void disposeControllers() {
    chewieController!.dispose();
    videoPlayerController!.dispose();
  }
}
```

In this code, we create a `VideoPlayerController` and a `ChewieController`. The `initializeVideo` method takes a URL as input and initializes the video player and chewie controller accordingly. The `disposeControllers` method disposes of the chewie and video player controllers.

Now, let's create a UI for video playback. In your main screen, add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';

import 'video_controller.dart';

class VideoScreen extends StatelessWidget {
  final videoController = Get.put(VideoController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Video Player'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            ElevatedButton(
              onPressed: () {
                videoController.initializeVideo('YOUR_VIDEO_URL');
                showDialog(
                  context: context,
                  builder: (_) => AlertDialog(
                    content: Chewie(controller: videoController.chewieController!),
                  ),
                );
              },
              child: Text('Play Video'),
            ),
          ],
        ),
      ),
    );
  }
}
```

In this code, we instantiate the `VideoController` using `Get.put` in the `videoController` variable. We create a UI with a button to play the video. Modify the `'YOUR_VIDEO_URL'` with the actual URL of the video file you want to play.

## Conclusion

In this blog post, we have explored how to use GetX for audio and video playback in Flutter. By leveraging the `audioplayers` and `chewie` packages along with GetX's state management capabilities, you can easily incorporate audio and video playback features into your Flutter applications. Start using GetX and take your multimedia experiences to the next level!

#flutter #GetX #multimedia #audioPlayback #videoPlayback