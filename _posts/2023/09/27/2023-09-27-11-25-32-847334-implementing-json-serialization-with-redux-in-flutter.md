---
layout: post
title: "Implementing JSON serialization with redux in Flutter"
description: " "
date: 2023-09-27
tags: [redux]
comments: true
share: true
---

In Flutter, using Redux as the state management solution can help you organize and manage your app's state efficiently. When dealing with APIs, it is common to work with JSON data. To seamlessly integrate JSON data with Redux in Flutter, you can follow these steps:

## Step 1: Define the JSON Model

First, define your JSON model. This model will represent the structure of the data you will retrieve from the API. Let's say you have an API endpoint that returns a list of `User` objects. Define the `User` model as follows:

```dart
class User {
  final int id;
  final String name;
  final String email;
  
  User({required this.id, required this.name, required this.email});
  
  factory User.fromJson(Map<String, dynamic> json) {
    return User(
      id: json['id'],
      name: json['name'],
      email: json['email'],
    );
  }
  
  Map<String, dynamic> toJson() {
    return {
      'id': id,
      'name': name,
      'email': email,
    };
  }
}
```

The `fromJson` factory method allows you to create a `User` object from a JSON Map, while the `toJson` method converts a `User` object back to a JSON Map.

## Step 2: Create Redux Actions

To handle the fetching and storing of JSON data using Redux, you will need to define Redux actions. Start by creating an action class, `FetchUsersAction`:

```dart
class FetchUsersAction {}

class SetUsersAction {
  final List<User> users;
  
  SetUsersAction(this.users);
}
```

The `FetchUsersAction` action triggers the API call to fetch the user data, while the `SetUsersAction` action stores the fetched user data in the Redux store.

## Step 3: Create Redux Reducers

Next, implement the reducers to handle the actions. In this example, you need to create a reducer to store the list of `User` objects:

```dart
List<User> usersReducer(List<User> state, dynamic action) {
  if (action is SetUsersAction) {
    return action.users;
  }
  
  return state;
}
```

The `usersReducer` function checks if the action is of type `SetUsersAction` and updates the state with the list of users.

## Step 4: Configure the Redux Store

To configure the Redux store, you need to combine the reducers and create the store. In your main.dart file, add the following code:

```dart
void main() {
  final store = Store<List<User>>(
    usersReducer,
    initialState: [],
  );

  runApp(App(store: store));
}
```

This sets up the initial state of the store as an empty list and assigns the `usersReducer` function to handle state updates.

## Step 5: Dispatch Actions

Now that Redux is set up to handle JSON serialization, you can dispatch actions. In this case, dispatch the `FetchUsersAction` to trigger the API call and the `SetUsersAction` to store the fetched user data:

```dart
class App extends StatelessWidget {
  final Store<List<User>> store;

  App({required this.store});

  @override
  Widget build(BuildContext context) {
    return StoreProvider<List<User>>(
      store: store,
      child: MaterialApp(
        ...
      ),
    );
  }
  
  Future<void> fetchUsers() async {
    final response = await http.get(Uri.parse('https://example.com/api/users'));
    final List<dynamic> jsonList = json.decode(response.body);
    
    final List<User> users = jsonList.map((json) => User.fromJson(json)).toList();
    
    store.dispatch(SetUsersAction(users));
  }
  
  // Call fetchUsers() where needed to trigger the API call
}
```

In the `fetchUsers` function, an HTTP request is made to retrieve the user data in JSON format. The JSON data is then parsed into a list of `User` objects using the `fromJson` factory method. Finally, the `SetUsersAction` is dispatched with the list of users to update the store.

With this implementation, you have successfully integrated JSON serialization with Redux in your Flutter app. You can now work with JSON data seamlessly while leveraging the power of Redux for state management.

#flutter #redux