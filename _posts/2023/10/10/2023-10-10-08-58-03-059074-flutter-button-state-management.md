---
layout: post
title: "Flutter button state management"
description: " "
date: 2023-10-10
tags: [StateManagement]
comments: true
share: true
---

In a Flutter application, buttons are vital for triggering user interactions. State management plays a crucial role in handling the different states of buttons, such as enabled, disabled, or loading. In this blog post, we will explore different approaches to managing the state of buttons in Flutter.

## Table of Contents
- [Local State Management](#local-state-management)
- [BLoC Pattern](#bloc-pattern)
- [Provider Package](#provider-package)
- [Conclusion](#conclusion)
- [#Flutter #StateManagement](#flutter-statemanagement)

## Local State Management

The simplest method of managing button state is by using local state management. Here, the state is stored within the widget itself and is updated whenever necessary. Let's take a look at an example:

```dart
class ButtonStateExample extends StatefulWidget {
  @override
  _ButtonStateExampleState createState() => _ButtonStateExampleState();
}

class _ButtonStateExampleState extends State<ButtonStateExample> {
  bool _isLoading = false;

  @override
  Widget build(BuildContext context) {
    return RaisedButton(
      onPressed: _isLoading ? null : _handleButtonPress,
      child: _isLoading 
          ? CircularProgressIndicator()
          : Text('Click Me'),
    );
  }

  void _handleButtonPress() async {
    setState(() {
      _isLoading = true;
    });

    // Perform some async task
    await Future.delayed(Duration(seconds: 2));

    setState(() {
      _isLoading = false;
    });
  }
}
```

In this example, we manage the state of the button using the `_isLoading` variable. When the button is pressed, we set `_isLoading` to true, which disables the button and displays a loading indicator. After the asynchronous task is completed, we set `_isLoading` back to false, enabling the button again.

## BLoC Pattern

The Business Logic Component (BLoC) pattern is a popular state management paradigm in Flutter. It separates the UI from the business logic by using streams and sinks to handle events and state changes. To manage button state using BLoC, we would create a stream of states and update the stream accordingly. Here's an example:

```dart
class ButtonStateBloc {
  final _isLoadingController = BehaviorSubject<bool>();

  Stream<bool> get isLoading => _isLoadingController.stream;

  void handleButtonPress() async {
    _isLoadingController.add(true);

    // Perform some async task
    await Future.delayed(Duration(seconds: 2));

    _isLoadingController.add(false);
  }

  void dispose() {
    _isLoadingController.close();
  }
}

class ButtonStateExample extends StatelessWidget {
  final bloc = ButtonStateBloc();

  @override
  Widget build(BuildContext context) {
    return StreamBuilder<bool>(
      stream: bloc.isLoading,
      initialData: false,
      builder: (context, snapshot) {
        return RaisedButton(
          onPressed: snapshot.data ? null : bloc.handleButtonPress,
          child: snapshot.data
              ? CircularProgressIndicator()
              : Text('Click Me'),
        );
      },
    );
  }

  @override
  void dispose() {
    bloc.dispose();
    super.dispose();
  }
}
```

In this example, we create a `ButtonStateBloc` class that manages the state of the button. We use a `BehaviorSubject` from the `rxdart` library to create a stream that emits the loading state. The `handleButtonPress` function updates the stream accordingly. In the `build` method, we use a `StreamBuilder` to listen to the stream and display the appropriate UI based on the emitted state.

## Provider Package

Another approach to handling button state in Flutter is by using the Provider package. Provider is a state management library that allows us to share data between widgets efficiently. With Provider, we can easily update the state of the button and listen for changes. Here's an example:

```dart
class ButtonStateModel extends ChangeNotifier {
  bool _isLoading = false;

  bool get isLoading => _isLoading;

  void handleButtonPress() async {
    _isLoading = true;
    notifyListeners();

    // Perform some async task
    await Future.delayed(Duration(seconds: 2));

    _isLoading = false;
    notifyListeners();
  }
}

class ButtonStateExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider<ButtonStateModel>(
      create: (_) => ButtonStateModel(),
      child: Consumer<ButtonStateModel>(
        builder: (context, model, _) {
          return RaisedButton(
            onPressed: model.isLoading ? null : model.handleButtonPress,
            child: model.isLoading
                ? CircularProgressIndicator()
                : Text('Click Me'),
          );
        },
      ),
    );
  }
}
```

In this example, we create a `ButtonStateModel` class that extends `ChangeNotifier` from the Provider package. The `isLoading` variable represents the state of the button. Whenever the state changes, we call `notifyListeners` to notify the consumers. In the `build` method, we use `ChangeNotifierProvider` to provide the `ButtonStateModel` to the widget tree and `Consumer` to listen for changes and update the UI accordingly.

## Conclusion

Managing button state is an essential aspect of a robust Flutter application. Whether you choose local state management, the BLoC pattern, or the Provider package, it's important to choose a method that suits your project's needs and complexity. By effectively managing button state, you can create delightful user experiences in your Flutter apps.

#Flutter #StateManagement