---
layout: post
title: "Implementing audio vocal removal with Flutter Sound"
description: " "
date: 2023-09-25
tags: [audio]
comments: true
share: true
---

Flutter Sound is a powerful audio plugin that allows you to record, play, and process audio in Flutter applications. In this blog post, we will explore how to implement audio vocal removal using Flutter Sound.

## What is Vocal Removal?

Vocal removal is a technique used to isolate or remove the vocals from an audio track, leaving only the instrumental elements. This can be useful in various scenarios, such as karaoke applications, remixing songs, or extracting background music from a recording.

## Getting Started

To begin, you'll need to set up a Flutter project and add the Flutter Sound plugin as a dependency. You can do this by adding the following line to your `pubspec.yaml` file:

```yaml
dependencies:
  flutter_sound: ^x.x.x # Replace with the latest version
```

Next, run `flutter packages get` to fetch the plugin. Now, you're ready to start implementing audio vocal removal.

## Processing Audio with Flutter Sound

Flutter Sound provides a variety of audio processing methods, including the ability to apply effects to an audio track. To remove vocals, we'll utilize the phase cancellation technique.

The phase cancellation technique works by taking two copies of the audio track: one with the original audio and another with an inverted version of the track. By adding these two tracks together, the vocals, which are typically mixed centrally, cancel each other out, leaving only the instrumental elements.

Here's an example code snippet demonstrating how to implement vocal removal with Flutter Sound:

```dart
import 'package:flutter_sound/flutter_sound.dart';

void removeVocals(String audioPath) async {
  FlutterSound flutterSound = FlutterSound();
  await flutterSound.openAudioSession();
  
  // Load the audio track
  int trackId = await flutterSound.startPlayer(audioPath);
  
  // Create a copy of the track with inverted phase
  await flutterSound.setPlayerWillPause(false);
  await flutterSound.setPlayerFeedCallback((Buffer buffer) async {
    // Invert the phase of the buffer
    for (var i = 0; i < buffer.writable; i++) {
      buffer.buffer[i] = buffer.buffer[i] * -1;
    }
    
    // Play the inverted track 
    await flutterSound.feedFromBuffer(buffer.buffer);
  });
  
  // Start playing the track
  await flutterSound.resumePlayer(trackId);
}
```

In the above code, we use the `FlutterSound` class to open an audio session and start playing the audio track. We then set up a callback function `setPlayerFeedCallback` to invert the phase of the audio buffer and play the inverted track. Finally, we resume the player to start playing the modified track.

## Conclusion

In this blog post, we explored how to implement audio vocal removal using Flutter Sound. By leveraging the phase cancellation technique, we can isolate or remove vocals from an audio track, leaving only the instrumental elements. Flutter Sound provides a powerful and flexible audio processing API, making it a great choice for implementing audio-related features in Flutter applications.

#flutter #audio #vocalremoval