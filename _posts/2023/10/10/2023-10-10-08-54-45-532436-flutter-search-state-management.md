---
layout: post
title: "Flutter search state management"
description: " "
date: 2023-10-10
tags: [search]
comments: true
share: true
---

When building applications, it's often necessary to implement search functionality to allow users to find specific data or information. In Flutter, there are various approaches to handle search functionality and manage the state of the search results. In this blog post, we'll explore some popular techniques for Flutter search state management.

## Table of Contents

1. [Local State Management](#local-state-management)
2. [Using Provider](#using-provider)
3. [BLoC Pattern](#bloc-pattern)
4. [Conclusion](#conclusion)

## Local State Management

One of the simplest ways to manage search state in Flutter is by using local state management. This approach involves keeping track of the search query and search results within the widget itself. Here's an example implementation:

```dart
class SearchWidget extends StatefulWidget {
  @override
  _SearchWidgetState createState() => _SearchWidgetState();
}

class _SearchWidgetState extends State<SearchWidget> {
  String searchQuery = '';
  List<String> searchResults = [];

  void onSearchTextChanged(String query) {
    setState(() {
      searchQuery = query;
      searchResults = performSearch(query);
    });
  }

  List<String> performSearch(String query) {
    // Perform search logic here
    // Return the search results
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        TextField(
          onChanged: onSearchTextChanged,
          decoration: InputDecoration(
            labelText: 'Search',
          ),
        ),
        ListView.builder(
          itemCount: searchResults.length,
          itemBuilder: (context, index) {
            return ListTile(
              title: Text(searchResults[index]),
            );
          },
        ),
      ],
    );
  }
}
```

In this example, the `_SearchWidgetState` class maintains the search query (`searchQuery`) and the search results (`searchResults`). The `onSearchTextChanged` function is called whenever the user types in the search text field, updating the search query and triggering a search operation. The results are displayed in a `ListView`.

## Using Provider

Another popular choice for search state management in Flutter is the `provider` package. This package allows for a more decoupled approach by separating the state management from the widget tree. Here's how you can implement search with `provider`:

```dart
class SearchModel extends ChangeNotifier {
  String searchQuery = '';
  List<String> searchResults = [];

  void updateSearchQuery(String query) {
    searchQuery = query;
    searchResults = performSearch(query);
    notifyListeners();
  }

  List<String> performSearch(String query) {
    // Perform search logic here
    // Return the search results
  }
}

class SearchWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final searchModel = Provider.of<SearchModel>(context);

    return Column(
      children: [
        TextField(
          onChanged: searchModel.updateSearchQuery,
          decoration: InputDecoration(
            labelText: 'Search',
          ),
        ),
        ListView.builder(
          itemCount: searchModel.searchResults.length,
          itemBuilder: (context, index) {
            return ListTile(
              title: Text(searchModel.searchResults[index]),
            );
          },
        ),
      ],
    );
  }
}
```

In this example, we define a `SearchModel` class that extends `ChangeNotifier` and holds the search query and results. The `updateSearchQuery` method updates the state and notifies listeners. In the `SearchWidget`, we use `Provider.of` to obtain an instance of `SearchModel` and bind the search query and results to the UI.

## BLoC Pattern

For more complex search scenarios and state management, the BLoC (Business Logic Component) pattern is a powerful approach. BLoC helps separate the presentation layer from the business logic and state management. The `flutter_bloc` library provides tools to implement the BLoC pattern in Flutter applications.

Implementing search with BLoC involves creating a `SearchBloc` that handles the search logic and exposes a `SearchState`. Here's an overview of how it could look:

```dart
class SearchState {}

class SearchIdleState extends SearchState {}

class SearchLoadingState extends SearchState {}

class SearchSuccessState extends SearchState {
  final List<String> searchResults;
  SearchSuccessState(this.searchResults);
}

class SearchFailureState extends SearchState {
  final String error;
  SearchFailureState(this.error);
}

class SearchEvent {}

class SearchTextChangedEvent extends SearchEvent {
  final String query;
  SearchTextChangedEvent(this.query);
}

class SearchBloc {
  final _controller = StreamController<SearchState>();
  Stream<SearchState> get searchState => _controller.stream;

  void onSearchTextChanged(String query) {
    // Perform search logic and emit the appropriate state
  }

  void dispose() {
    _controller.close();
  }
}

class SearchWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final searchBloc = BlocProvider.of<SearchBloc>(context);

    return Column(
      children: [
        TextField(
          onChanged: (query) =>
              searchBloc.add(SearchTextChangedEvent(query)),
          decoration: InputDecoration(
            labelText: 'Search',
          ),
        ),
        BlocBuilder<SearchBloc, SearchState>(
          builder: (context, state) {
            if (state is SearchLoadingState) {
              return CircularProgressIndicator();
            }

            if (state is SearchSuccessState) {
              return ListView.builder(
                itemCount: state.searchResults.length,
                itemBuilder: (context, index) {
                  return ListTile(
                    title: Text(state.searchResults[index]),
                  );
                },
              );
            }

            if (state is SearchFailureState) {
              return Text("Error: ${state.error}");
            }

            return Container();
          },
        ),
      ],
    );
  }
}
```

In this example, the `SearchBloc` handles the search logic and exposes a `searchState` stream. When the search text changes, an appropriate `SearchEvent` is dispatched to the bloc. The `BlocBuilder` listens to changes in the search state and rebuilds the UI accordingly.

## Conclusion

Managing search state effectively is crucial for providing a seamless user experience in Flutter applications. Depending on the complexity of your app and the requirements of your search functionality, you can choose between local state management, `provider`, or the BLoC pattern. Each approach has its own strengths and trade-offs. Experiment with different methods to find the one that fits best for your use case.

#flutter #search