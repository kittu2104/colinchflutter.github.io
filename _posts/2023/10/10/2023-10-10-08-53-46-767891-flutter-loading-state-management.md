---
layout: post
title: "Flutter loading state management"
description: " "
date: 2023-10-10
tags: [loadingstates]
comments: true
share: true
---

When developing a Flutter application, it's common to encounter scenarios where you need to handle loading states. Loading states occur when you are fetching data from an API, performing complex calculations, or waiting for a response from a database.

Handling loading states correctly ensures a smooth user experience and prevents the application from freezing or becoming unresponsive.

In this article, we will explore different approaches to managing loading states in Flutter applications.

## Table of Contents
- [StatefulWidget](#StatefulWidget)
- [Provider Package](#Provider-Package)
- [BLoC Pattern](#BLoC-Pattern)
- [Conclusion](#Conclusion)

## StatefulWidget

The simplest way to manage loading states in a Flutter application is by using the `StatefulWidget`. With this approach, you define a boolean flag to track the loading state and update the UI accordingly.

Here's an example of how you can use a `StatefulWidget` to manage loading states:

```dart
class MyWidget extends StatefulWidget {
  @override
  _MyWidgetState createState() => _MyWidgetState();
}

class _MyWidgetState extends State<MyWidget> {
  bool _isLoading = false;

  Future<void> fetchData() async {
    setState(() {
      _isLoading = true;
    });

    // Perform data fetching here

    setState(() {
      _isLoading = false;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: _isLoading
            ? CircularProgressIndicator()
            : RaisedButton(
                onPressed: fetchData,
                child: Text('Fetch Data'),
              ),
      ),
    );
  }
}
```

In the code above, the `_isLoading` variable is used to track the loading state. The UI is updated based on this variable, showing a circular progress indicator when loading and a button otherwise.

## Provider Package

Another popular approach to managing loading states in Flutter is by using the `provider` package. The provider package is a state management solution that allows you to easily propagate changes in the application state.

To manage loading states using the provider package, follow these steps:

1. Create a separate class to hold the loading state:

```dart
class LoadingState extends ChangeNotifier {
  bool _isLoading = false;

  bool get isLoading => _isLoading;

  void startLoading() {
    _isLoading = true;
    notifyListeners();
  }

  void stopLoading() {
    _isLoading = false;
    notifyListeners();
  }
}
```

2. Provide the loading state using the `Provider` widget:

```dart
class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (_) => LoadingState(),
      child: MaterialApp(
        ...
      ),
    );
  }
}
```

3. Consume the loading state within a widget:

```dart
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final loadingState = Provider.of<LoadingState>(context);

    return Scaffold(
      body: Center(
        child: loadingState.isLoading
            ? CircularProgressIndicator()
            : RaisedButton(
                onPressed: () {
                  loadingState.startLoading();
                  // Perform data fetching here
                  loadingState.stopLoading();
                },
                child: Text('Fetch Data'),
              ),
      ),
    );
  }
}
```

By using the provider package, you can easily propagate changes in the loading state, allowing various widgets to react accordingly.

## BLoC Pattern

The BLoC (Business Logic Component) pattern is another powerful approach to manage loading states in Flutter. It separates the application's business logic from the UI, making the code more maintainable and testable.

Here's an example of how to implement the BLoC pattern for managing loading states:

```dart
class DataBloc {
  Stream<bool> get loadingState => _loadingStateController.stream;

  final _loadingStateController = StreamController<bool>();

  void fetchData() async {
    _loadingStateController.add(true);

    // Perform data fetching here

    _loadingStateController.add(false);
  }

  void dispose() {
    _loadingStateController.close();
  }
}

class MyWidget extends StatelessWidget {
  final DataBloc _dataBloc = DataBloc();

  @override
  Widget build(BuildContext context) {
    return StreamBuilder<bool>(
      stream: _dataBloc.loadingState,
      initialData: false,
      builder: (context, snapshot) {
        return Scaffold(
          body: Center(
            child: snapshot.data
                ? CircularProgressIndicator()
                : RaisedButton(
                    onPressed: _dataBloc.fetchData,
                    child: Text('Fetch Data'),
                  ),
          ),
        );
      },
    );
  }

  @override
  void dispose() {
    _dataBloc.dispose();
    super.dispose();
  }
}
```

In the code above, the `DataBloc` class handles the loading state using a stream. The UI updates based on the stream's value, displaying either a progress indicator or a button.

## Conclusion

Handling loading states is crucial for providing a good user experience in Flutter applications. In this article, we explored different approaches, including using `StatefulWidget`, the `provider` package, and the BLoC pattern.

Choose the approach that best fits your project's requirements and complexity. Remember to always consider scalability and code maintainability when managing loading states. #flutter #loadingstates