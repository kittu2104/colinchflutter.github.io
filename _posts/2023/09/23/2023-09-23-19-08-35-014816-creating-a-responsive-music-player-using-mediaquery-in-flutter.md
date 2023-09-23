---
layout: post
title: "Creating a responsive music player using `MediaQuery` in Flutter"
description: " "
date: 2023-09-23
tags: [flutter, responsiveness]
comments: true
share: true
---

In this tutorial, we will learn how to create a responsive music player using the `MediaQuery` class in Flutter. `MediaQuery` allows us to obtain the size and orientation of the device's screen, and based on that, we can adjust the UI of our app accordingly.

Let's get started by creating a new Flutter project:

1. Open your preferred IDE.
2. Create a new Flutter project using the `flutter create` command.

Now, let's dive into the implementation:

1. Open the `lib/main.dart` file.

2. Inside the `build` method of the `MyApp` class, wrap the `MaterialApp` with a `Builder` widget.

```dart
@override
Widget build(BuildContext context) {
  return Builder(
    builder: (BuildContext context) {
      return MaterialApp(
        title: 'Responsive Music Player',
        home: MyHomePage(),
      );
    },
  );
}
```

3. Create a new widget called `MyHomePage`. This will be the main screen of our music player.

```dart
class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Music Player'),
      ),
      body: Center(
        child: Text('Responsive Music Player'),
      ),
    );
  }
}
```

4. Inside the `body` property of the `Scaffold`, we will use `MediaQuery` to adjust the UI based on the screen size.

```dart
body: Center(
  child: MediaQuery.of(context).size.width >= 600 ? _buildWideLayout() : _buildNarrowLayout(),
),
```

5. Create two separate methods, `_buildWideLayout` and `_buildNarrowLayout`, to provide different layouts for wide and narrow screens, respectively.

```dart
Widget _buildWideLayout() {
  return Container(
    child: Row(
      children: [
        Expanded(
          flex: 2,
          child: Container(
            color: Colors.blue,
            height: double.infinity,
            child: VerticalMenu(),
          ),
        ),
        Expanded(
          flex: 3,
          child: Container(
            color: Colors.white,
            height: double.infinity,
            child: MusicList(),
          ),
        ),
        Expanded(
          flex: 4,
          child: Container(
            color: Colors.grey,
            height: double.infinity,
            child: MusicDetail(),
          ),
        ),
      ],
    ),
  );
}

Widget _buildNarrowLayout() {
  return Column(
    children: [
      Expanded(
        flex: 2,
        child: Container(
          color: Colors.blue,
          width: double.infinity,
          child: HorizontalMenu(),
        ),
      ),
      Expanded(
        flex: 4,
        child: Container(
          color: Colors.white,
          width: double.infinity,
          child: MusicList(),
        ),
      ),
      Expanded(
        flex: 5,
        child: Container(
          color: Colors.grey,
          width: double.infinity,
          child: MusicDetail(),
        ),
      ),
    ],
  );
}
```

6. Lastly, you can create separate widgets, such as `VerticalMenu`, `HorizontalMenu`, `MusicList`, and `MusicDetail`, to display the actual content of your music player based on different screen sizes.

That's it! You have successfully created a responsive music player using `MediaQuery` in Flutter. With this implementation, your app will adjust its layout dynamically based on the screen size of the device.

Remember to test your app on different devices and screen orientations to ensure it adapts correctly.

#flutter #responsiveness