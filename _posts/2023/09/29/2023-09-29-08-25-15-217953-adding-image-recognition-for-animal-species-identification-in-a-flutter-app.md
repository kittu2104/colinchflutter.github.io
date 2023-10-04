---
layout: post
title: "Adding image recognition for animal species identification in a Flutter app"
description: " "
date: 2023-09-29
tags: [imageRecognition]
comments: true
share: true
---

In this blog post, we will explore how to integrate image recognition for animal species identification into a Flutter app. Image recognition allows us to analyze and classify images using machine learning models, enabling us to identify different animal species based on the images provided.

## Why Use Image Recognition for Animal Species Identification?

Image recognition has become a powerful tool in various domains, including wildlife conservation and animal research. By using image recognition, we can quickly and accurately identify different animal species, making it easier to track populations, monitor endangered species, and conduct research studies.

## Getting Started

To begin, we need to set up our Flutter project and install the necessary packages. Open your terminal and navigate to your project directory. Run the following command to create a new Flutter project:

```
flutter create animal_species_identification
```

Next, navigate into the project directory:

```
cd animal_species_identification
```

To use image recognition capabilities, we will use the *tflite* package in Flutter. Add the following line to the `dependencies` section in your `pubspec.yaml` file:

```yaml
dependencies:
  tflite: ^1.0.3
```

Save the file and run the following command to fetch the package:

```
flutter pub get
```

## Preparing the Machine Learning Model

To perform image recognition, we need a pre-trained machine learning model that can classify animal species. There are various models available, such as MobileNet and Inception, which have been trained on large datasets. For this tutorial, we will use the MobileNet model.

Download the MobileNet model by clicking [here](https://www.tensorflow.org/lite/models/image_classification/overview). Extract the model file and place it in the project folder.

## Implementing Image Recognition in the Flutter App

Now let's start implementing image recognition in our Flutter app. Open the `main.dart` file and modify it as follows:

```dart
import 'package:flutter/material.dart';
import 'package:image_picker/image_picker.dart';
import 'package:tflite/tflite.dart';

void main() {
  runApp(MaterialApp(
    home: AnimalSpeciesIdentification(),
  ));
}

class AnimalSpeciesIdentification extends StatefulWidget {
  @override
  _AnimalSpeciesIdentificationState createState() => _AnimalSpeciesIdentificationState();
}

class _AnimalSpeciesIdentificationState extends State<AnimalSpeciesIdentification> {
  List<dynamic> _recognitions;
  bool _isLoading = false;

  @override
  void initState() {
    super.initState();
    loadModel();
  }

  void loadModel() async {
    await Tflite.loadModel(
      model: 'assets/mobilenet.tflite',
      labels: 'assets/labels.txt',
    );
  }

  void classifyImage() async {
    setState(() {
      _isLoading = true;
    });

    var image = await ImagePicker().getImage(
      source: ImageSource.gallery,
    );

    if (image != null) {
      var recognitions = await Tflite.runModelOnImage(
        path: image.path,
        numResults: 3,
        threshold: 0.2,
      );

      setState(() {
        _recognitions = recognitions;
        _isLoading = false;
      });
    } else {
      setState(() {
        _isLoading = false;
      });
    }
  }

  @override
  void dispose() {
    Tflite.close();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Animal Species Identification'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            _isLoading
                ? CircularProgressIndicator()
                : RaisedButton(
                    onPressed: classifyImage,
                    child: Text('Choose an Image'),
                  ),
            SizedBox(height: 20),
            _recognitions != null
                ? Column(
                    children: [
                      Image.asset(
                        _recognitions[0]['index'] == 0
                            ? 'assets/images/cat.jpg'
                            : 'assets/images/dog.jpg',
                        height: 200,
                      ),
                      SizedBox(height: 20),
                      Text(
                        'Prediction: ${_recognitions[0]['label']} (${(_recognitions[0]['confidence'] * 100).toStringAsFixed(2)}%)',
                      ),
                    ],
                  )
                : SizedBox(),
          ],
        ),
      ),
    );
  }
}
```

In the above code, we have defined a Flutter app with a single screen. The app uses the `image_picker` package to select an image from the gallery. The selected image is then passed to the `Tflite.runModelOnImage` method to classify the animal species using the MobileNet model.

Remember to place the image files you want to test in the `assets/images` folder and update the file paths accordingly in the code.

## Running the App

To run the app on your device or simulator, use the following command:

```
flutter run
```

You should now see the app running on your device or simulator. Tap the "Choose an Image" button to select an image from your gallery. The app will then classify the animal species and display the prediction along with the confidence level.

## Conclusion

Integrating image recognition for animal species identification in a Flutter app can greatly enhance wildlife conservation efforts and research studies. By leveraging the power of machine learning models, we can accurately identify different animal species based on the images provided. With the code provided in this blog post, you can now start building your own image recognition capabilities in your Flutter apps.

#flutter #imageRecognition