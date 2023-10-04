---
layout: post
title: "Drawing with particles in Flutter"
description: " "
date: 2023-10-04
tags: [setting, creating]
comments: true
share: true
---

In this tutorial, we will explore how to create a particle effect in Flutter using the `CustomPainter` class. We will be drawing particles on a canvas by leveraging the power of Flutter's animation and painting APIs. So, let's dive in and create a captivating particle effect!

## Table of Contents
- [Setting Up the Project](#setting-up-the-project)
- [Creating a Particle Model](#creating-a-particle-model)
- [Building the Particle Widget](#building-the-particle-widget)
- [Animating Particle Movement](#animating-particle-movement)
- [Drawing Particles on Canvas](#drawing-particles-on-canvas)
- [Conclusion](#conclusion)

## Setting Up the Project

Start by creating a new Flutter project using your preferred IDE or the command line:

```dart
flutter create particle_effect
```

Next, open the `pubspec.yaml` file and add the following dependency:

```yaml
dependencies:
  flutter:
    sdk: flutter

  vector_math: ^2.1.0
```

Save the file and run `flutter packages get` to fetch the new dependency.

## Creating a Particle Model

Create a new file called `particle.dart` and define the `Particle` class:

```dart
import 'package:flutter/material.dart';
import 'package:vector_math/vector_math_64.dart' as vmath;

class Particle {
  vmath.Vector2 position;
  vmath.Vector2 velocity;
  double radius;
  Color color;

  Particle(this.position, this.velocity, this.radius, this.color);
}
```

The `Particle` class represents a single particle with its position, velocity, radius, and color.

## Building the Particle Widget

Create a new file called `particle_widget.dart` and define the `ParticleWidget` class:

```dart
import 'dart:ui';

import 'package:flutter/material.dart';
import 'package:particle_effect/particle.dart';

class ParticleWidget extends StatefulWidget {
  @override
  _ParticleWidgetState createState() => _ParticleWidgetState();
}

class _ParticleWidgetState extends State<ParticleWidget>
    with SingleTickerProviderStateMixin {
  AnimationController _animationController;
  List<Particle> _particles;

  @override
  void initState() {
    super.initState();
    _animationController = AnimationController(
      vsync: this,
      duration: Duration(seconds: 1),
    )..repeat();

    _particles = List.generate(
      100,
      (_) => Particle(
        Offset.zero,
        Offset(
          _random.nextDouble() * 2 - 1,
          _random.nextDouble() * 2 - 1,
        ),
        _random.nextDouble() * 2 + 1,
        Colors.white,
      ),
    );
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return AnimatedBuilder(
      animation: _animationController,
      builder: (context, child) {
        _updateParticles();
        return CustomPaint(
          painter: ParticlePainter(_particles),
        );
      },
    );
  }

  void _updateParticles() {
    final double width = window.physicalSize.width / window.devicePixelRatio;
    final double height = window.physicalSize.height / window.devicePixelRatio;

    for (final particle in _particles) {
      // Update particle position based on velocity
      particle.position += particle.velocity;

      // Wrap particles around the screen
      if (particle.position.dx < 0) {
        particle.position = Offset(width, particle.position.dy);
      }
      if (particle.position.dx > width) {
        particle.position = Offset(0, particle.position.dy);
      }
      if (particle.position.dy < 0) {
        particle.position = Offset(particle.position.dx, height);
      }
      if (particle.position.dy > height) {
        particle.position = Offset(particle.position.dx, 0);
      }
    }
  }
}

class ParticlePainter extends CustomPainter {
  List<Particle> particles;

  ParticlePainter(this.particles);

  @override
  void paint(Canvas canvas, Size size) {
    for (final particle in particles) {
      canvas.drawCircle(
        particle.position,
        particle.radius,
        Paint()..color = particle.color,
      );
    }
  }

  @override
  bool shouldRepaint(ParticlePainter oldDelegate) => true;
}
```

The `ParticleWidget` class is a stateful widget that manages the animation and particle rendering. It uses the `CustomPainter` class to draw the particles on the canvas.

## Animating Particle Movement

To animate the movement of particles, we will use the `AnimationController` class. Add the following code inside the `_ParticleWidgetState` class:

```dart
AnimationController _animationController;

@override
void initState() {
  super.initState();
  _animationController = AnimationController(
    vsync: this,
    duration: Duration(seconds: 1),
  )..repeat();
}

@override
void dispose() {
  _animationController.dispose();
  super.dispose();
}
```

The animation controller is set to repeat and has a duration of 1 second.

## Drawing Particles on Canvas

To draw the particles on the canvas, we need to implement the `CustomPainter` class. Add the following code inside the `_ParticleWidgetState` class:

```dart
class ParticlePainter extends CustomPainter {
  List<Particle> particles;

  ParticlePainter(this.particles);

  @override
  void paint(Canvas canvas, Size size) {
    for (final particle in particles) {
      canvas.drawCircle(
        particle.position,
        particle.radius,
        Paint()..color = particle.color,
      );
    }
  }

  @override
  bool shouldRepaint(ParticlePainter oldDelegate) => true;
}
```

The `ParticlePainter` class is responsible for painting the particles on the canvas. We iterate through the list of particles and use the `drawCircle` method to draw a circle at each particle's position.

## Conclusion

In this tutorial, we explored how to create a particle effect in Flutter by leveraging the `CustomPainter` class. We built a particle widget that animates and renders particles on a canvas. Feel free to experiment with different particle properties and styles to create your own unique particle effects in Flutter!

#flutter #particle-effect