---
layout: post
title: "Implementing server-side search functionality in Flutter SSR"
description: " "
date: 2023-09-21
tags: [flutter, server_side_search, FlutterSSR, search]
comments: true
share: true
---

In this article, we will explore how to implement server-side search functionality in a Flutter server-side rendering (SSR) application. Adding search functionality to your app is crucial to improve user experience and make your app more interactive.

## Setting up the Flutter SSR Project

First, make sure you have a Flutter SSR project set up. If not, you can create one by running the following command:

```bash
flutter create --template=server project_name
```

## Implementing the Server-Side Search Endpoint

Next, we need to create an endpoint on the server that will handle the search functionality. Create a new file called `search_endpoint.dart` and add the following code:

```dart
import 'package:shelf/shelf.dart';
import 'package:shelf_router/shelf_router.dart';

class SearchEndpoint {
  Router get router {
    final router = Router();

    router.post('/search', (Request request) async {
      final requestBody = await request.readAsString();
      // Process the search query and return the search results
      final searchResults = await performSearch(requestBody);

      return Response.ok(searchResults);
    });

    return router;
  }

  Future<List<String>> performSearch(String queryString) {
    // Implement your search logic here
    // Perform search query on database or any other data source
    
    // Return search results
    
    return Future.value([]);
  }
}
```

The `search` endpoint listens for a POST request and expects a JSON payload containing the search query. Upon receiving the request, the `performSearch` method is called to process the search query and return the search results. You can implement your custom search logic in this method.

## Adding Client-Side Search Widget

Now, let's integrate the server-side search functionality into your Flutter SSR application. Open your main.dart file and add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_ssr_example/search_endpoint.dart';
import 'package:shelf/shelf.dart' as shelf;
import 'package:shelf/shelf_io.dart' as shelf_io;
import 'package:shelf_static/shelf_static.dart';

void main() async {
  final app = MyApp();
  
  // Configure server
  final cascade = shelf.Cascade().add(app.router.middleware);
  final handler = shelf_io.createServer(cascade.handler);

  // Start server
  await handler.serve();
}

class MyApp {
  final router = Router();

  MyApp() {
    // Adding the search endpoint
    router.mount('/api/', SearchEndpoint().router);

    // ... other route handlers
  }

  shelf.Response Function(shelf.Request) get handleRequest {
    return router.handler;
  }

  //... rest of the app code
}
```

In the above code, we create a `SearchEndpoint` instance and mount it on the `/api/` path using the `router.mount` method. This allows our SSR application to communicate with the server-side search endpoint.

## Consuming the Search Endpoint on the Client-Side

To consume the server-side search endpoint in your Flutter SSR application, you can use the `http` package to make HTTP POST requests. Here's an example of how you can use it:

```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;

class SearchScreen extends StatefulWidget {
  @override
  _SearchScreenState createState() => _SearchScreenState();
}

class _SearchScreenState extends State<SearchScreen> {
  TextEditingController _searchController = TextEditingController();
  List<String> _searchResults = [];

  void _performSearch() async {
    final response = await http.post(Uri.parse('/api/search'),
        body: {'query': _searchController.text});
    
    if (response.statusCode == 200) {
      setState(() {
        _searchResults = response.body as List<String>;
      });
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Search'),
      ),
      body: Column(
        children: [
          TextField(
            controller: _searchController,
            decoration: InputDecoration(
              hintText: 'Enter search query',
            ),
          ),
          ElevatedButton(
            onPressed: _performSearch,
            child: Text('Search'),
          ),
          // Display search results
          ListView.builder(
            itemCount: _searchResults.length,
            itemBuilder: (context, index) {
              return ListTile(
                title: Text(_searchResults[index]),
              );
            },
          )
        ],
      ),
    );
  }
}
```

In the above code, we create a simple search screen with a text field and a button. On button press, we make an HTTP POST request to the `/api/search` endpoint with the query parameter. The server-side search results are then displayed in a ListView widget.

## Conclusion

Implementing server-side search functionality in a Flutter SSR application is a great way to enhance user experience and improve application performance. By choosing a good server-side search architecture and following the steps outlined in this article, you can easily integrate powerful search capabilities into your Flutter SSR app.

#flutter #SSR #server_side_search #FlutterSSR #search