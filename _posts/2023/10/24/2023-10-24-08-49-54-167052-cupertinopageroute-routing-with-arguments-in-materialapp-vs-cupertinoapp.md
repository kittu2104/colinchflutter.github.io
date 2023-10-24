---
layout: post
title: "CupertinoPageRoute routing with arguments in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When implementing navigation in a Flutter app, we have two options: MaterialApp and CupertinoApp. Both provide routing functionalities, allowing us to navigate between different screens or pages. In this article, we will focus on the differences in passing arguments while navigating using the CupertinoPageRoute in MaterialApp and CupertinoApp.

## Routing with arguments in MaterialApp

The MaterialApp widget is the most commonly used widget for building Flutter apps. It provides a material-themed app and includes various features, including routing. When using MaterialPageRoute in MaterialApp, passing arguments to a new screen is straight-forward.

Let's say we have a "DetailsScreen" that requires some data to be passed from the previous screen. We can achieve this by passing the arguments with the help of the MaterialPageRoute's constructor. Here's an example code snippet demonstrating how to pass arguments in the MaterialApp:

```dart
class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home'),
      ),
      body: Center(
        child: ElevatedButton(
          child: Text('Go to Details'),
          onPressed: () {
            Navigator.push(
              context,
              MaterialPageRoute(
                builder: (context) => DetailsScreen(
                  name: 'John Doe',
                  age: 25,
                ),
              ),
            );
          },
        ),
      ),
    );
  }
}

class DetailsScreen extends StatelessWidget {
  final String name;
  final int age;

  DetailsScreen({required this.name, required this.age});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Details'),
      ),
      body: Container(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Name: $name'),
            Text('Age: $age'),
          ],
        ),
      ),
    );
  }
}
```

In the above code, we pass the name 'John Doe' and age 25 as arguments while navigating to the DetailsScreen. These arguments are then used to display the name and age on the DetailsScreen.

## Routing with arguments in CupertinoApp 

CupertinoApp, on the other hand, provides a Cupertino-themed app, following the iOS design guidelines. When using the CupertinoPageRoute in CupertinoApp, the process of passing arguments is slightly different.

Instead of directly passing arguments through the constructor of the CupertinoPageRoute, we can make use of onGenerateRoute and RouteSettings to achieve the same result. Here's an example code snippet demonstrating how to pass arguments in the CupertinoApp:

```dart
class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Home'),
      ),
      child: Center(
        child: CupertinoButton(
          child: Text('Go to Details'),
          onPressed: () {
            Navigator.of(context).push(
              CupertinoPageRoute(
                builder: (context) => DetailsScreen(),
                settings: RouteSettings(
                  arguments: {
                    'name': 'John Doe',
                    'age': 25,
                  },
                ),
              ),
            );
          },
        ),
      ),
    );
  }
}

class DetailsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final args = ModalRoute.of(context)?.settings.arguments as Map<String, dynamic>?;

    final name = args?['name'];
    final age = args?['age'];

    return CupertinoPageScaffold(
      navigationBar: CupertinoNavigationBar(
        middle: Text('Details'),
      ),
      child: Container(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text('Name: $name'),
            Text('Age: $age'),
          ],
        ),
      ),
    );
  }
}
```

In the above code, we pass the arguments 'name' and 'age' through the RouteSettings of the CupertinoPageRoute while navigating to the DetailsScreen. Inside the DetailsScreen, we retrieve the arguments using ModalRoute and RouteSettings.

## Conclusion

Both MaterialApp and CupertinoApp provide routing functionalities for Flutter navigation. However, when it comes to passing arguments, there are some differences. When using MaterialPageRoute in MaterialApp, we can pass arguments directly through the constructor. On the other hand, when using CupertinoPageRoute in CupertinoApp, we need to utilize onGenerateRoute and RouteSettings to pass and retrieve arguments.

Understanding these differences can help you choose the appropriate approach based on your app's design and platform requirements.