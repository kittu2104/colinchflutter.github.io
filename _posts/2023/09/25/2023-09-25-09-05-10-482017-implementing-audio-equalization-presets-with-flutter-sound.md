---
layout: post
title: "Implementing audio equalization presets with Flutter Sound"
description: " "
date: 2023-09-25
tags: [audiosound]
comments: true
share: true
---

## Setting up Flutter Sound
To get started, you'll need to add the Flutter Sound dependency to your pubspec.yaml file. Open your pubspec.yaml and add the following line under the `dependencies` section:

```yaml
dependencies:
  flutter_sound: ^X.X.X
```

Replace `X.X.X` with the latest version of Flutter Sound.

After adding the dependency, run `flutter pub get` to fetch the package.

## Implementing audio equalization presets
1. Import the necessary packages:

```dart
import 'package:flutter_sound/flutter_sound.dart';
import 'package:flutter_sound/flutter_sound.dart';
```

2. Create an instance of Flutter Sound:

```dart
FlutterSoundPlayer _audioPlayer = FlutterSoundPlayer();
```

3. Load the audio file to be played:

```dart
await _audioPlayer.openAudioSession();
await _audioPlayer.startPlayer(fromURI: 'path_to_audio_file');
```

Make sure to replace `path_to_audio_file` with the actual path to your audio file.

4. Implement the equalization presets:

```dart
void applyEqualizationPreset(EqPreset preset) {
  for (int i = 0; i < preset.bands.length; i++) {
    final band = preset.bands[i];
    _audioPlayer.setEQ(i, FlutterSound.ULOWPASS_FREQ, band.lowPassFrequency);
    _audioPlayer.setEQ(i, FlutterSound.UHIGHPASS_FREQ, band.highPassFrequency);
    _audioPlayer.setEQ(i, FlutterSound.UBAND_FREQ, band.frequency);
    _audioPlayer.setEQBand(i, FlutterSound.UBAND_GAIN, band.gain);
    _audioPlayer.setEQBand(i, FlutterSound.UBAND_BW_OCT, band.bandwidth);
  }
}
```

This function applies the equalization preset to the audio player. It loops through each band in the preset and sets the corresponding equalizer parameters using the Flutter Sound API.

5. Create and apply the desired equalization presets:

```dart
EqPreset bassBoostPreset = EqPreset(
  bands: [
    EqPresetBand(lowPassFrequency: 300, highPassFrequency: 20000, frequency: 60, gain: 6, bandwidth: 1),
    EqPresetBand(lowPassFrequency: 300, highPassFrequency: 20000, frequency: 170, gain: 4, bandwidth: 1),
    EqPresetBand(lowPassFrequency: 300, highPassFrequency: 20000, frequency: 310, gain: 2, bandwidth: 1),
  ],
);

applyEqualizationPreset(bassBoostPreset);
```

This example creates a bass boost preset with three bands. Adjust the values of the bands to achieve the desired equalization effect.

## Conclusion
By implementing audio equalization presets with Flutter Sound, you can offer your users more control over their audio experience. They can choose from various presets or create their own custom settings. Experiment with different equalization presets to find the perfect sound for your audio playback.

Remember to include the necessary code snippets and replace `X.X.X` with the proper version number.

#flutter #audiosound