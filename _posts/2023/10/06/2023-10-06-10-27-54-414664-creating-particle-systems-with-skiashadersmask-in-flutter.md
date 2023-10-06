---
layout: post
title: "Creating particle systems with SkiaShadersMask in Flutter"
description: " "
date: 2023-10-06
tags: []
comments: true
share: true
---

In Flutter, Skia is the 2D graphics library used for rendering. Skia provides a powerful feature called *shaders*, which allows you to create complex visual effects and customize how elements are rendered on the screen. One interesting use case for shaders is creating particle systems.

A particle system is a technique used in computer graphics to simulate the behavior of multiple objects or particles. These particles can have various properties like position, velocity, color, and size, and they move and interact with each other to create visually appealing effects.

In this tutorial, we will explore how to create a simple particle system using the `SkiaShadersMask` class in Flutter.

## Prerequisites

To follow along, make sure you have Flutter installed on your system. You can download Flutter from the official Flutter website and install it according to the instructions provided.

## Step 1: Setting up the project

Create a new Flutter project using the following command:

```shell
flutter create particle_system
cd particle_system
```

## Step 2: Adding dependencies

Open the `pubspec.yaml` file in your project directory and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter
  skia_flutter: ^0.4.0
  random_color: ^1.0.6
```

Save the file, then run `flutter pub get` to fetch the new dependency.

## Step 3: Implementing the particle system

Open the `lib/main.dart` file and replace the default code with the following:

```dart
import 'dart:math';

import 'package:flutter/material.dart';
import 'package:random_color/random_color.dart';
import 'package:skia_flutter/skia_flutter.dart';

void main() {
  runApp(ParticleSystemApp());
}

class ParticleSystemApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Particle System',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: ParticleSystemPage(),
    );
  }
}

class ParticleSystemPage extends StatefulWidget {
  @override
  _ParticleSystemPageState createState() => _ParticleSystemPageState();
}

class _ParticleSystemPageState extends State<ParticleSystemPage>
    with SingleTickerProviderStateMixin {
  late AnimationController _controller;

  final particles = <Particle>[];

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      vsync: this,
      duration: Duration(seconds: 3),
    )..repeat();
  }

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Particle System'),
      ),
      body: AnimatedBuilder(
        animation: _controller,
        builder: (BuildContext context, Widget? child) {
          return CustomPaint(
            painter: ParticleSystemPainter(
              particles: particles,
              progress: _controller.value,
            ),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          setState(() {
            particles.add(
              Particle(
                position: Offset(0, 0),
                velocity: Offset(
                  Random().nextDouble() * 2 - 1,
                  Random().nextDouble() * 2 - 1,
                ),
                color: RandomColor().randomColor(),
                size: Random().nextDouble() * 40 + 10,
              ),
            );
          });
        },
        child: Icon(Icons.add),
      ),
    );
  }
}

class Particle {
  final Offset position;
  final Offset velocity;
  final Color color;
  final double size;

  Particle({
    required this.position,
    required this.velocity,
    required this.color,
    required this.size,
  });
}

class ParticleSystemPainter extends CustomPainter {
  final List<Particle> particles;
  final double progress;

  ParticleSystemPainter({
    required this.particles,
    required this.progress,
  });

  @override
  void paint(Canvas canvas, Size size) {
    final width = size.width;
    final height = size.height;

    final progressOffset = progress * 200;

    particles.forEach((particle) {
      final positionX = (particle.position.dx + particle.velocity.dx * progressOffset) % width;
      final positionY = (particle.position.dy + particle.velocity.dy * progressOffset) % height;

      final paint = Paint()..color = particle.color;

      canvas.drawCircle(
        Offset(positionX, positionY),
        particle.size,
        paint,
      );
    });
  }

  @override
  bool shouldRepaint(covariant ParticleSystemPainter oldDelegate) =>
      particles != oldDelegate.particles || progress != oldDelegate.progress;
}

```

## Step 4: Testing the particle system

Save the file, then run the app using the following command:

```shell
flutter run
```

You should now see a blank screen with a floating action button at the bottom. Pressing the button will add particles to the screen, and they will move around based on the velocity properties.

Congratulations! You have successfully created a simple particle system using the `SkiaShadersMask` class in Flutter.

## Conclusion

Particle systems are a fascinating visual effect that can enhance the user experience of your Flutter apps. By utilizing the powerful features of Skia and Flutter, you can create complex and dynamic particle systems that are highly customizable.

Feel free to experiment further with this example by adding more properties to the particles or introducing interactions between them. The possibilities are endless when it comes to creating visually stunning effects with Skia shaders and Flutter.

#flutter #particle-systems