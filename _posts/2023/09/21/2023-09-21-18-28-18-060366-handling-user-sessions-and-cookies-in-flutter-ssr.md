---
layout: post
title: "Handling user sessions and cookies in Flutter SSR"
description: " "
date: 2023-09-21
tags: [flutter]
comments: true
share: true
---

User sessions and cookies are essential for creating stateful applications, and Flutter for Server-Side Rendering (SSR) allows us to build dynamic server-rendered web applications using Flutter.

In this blog post, we'll explore how to handle user sessions and cookies in Flutter SSR applications.

## What are User Sessions and Cookies?

A user session represents a series of interactions between a user and a server within a specific time frame. Sessions allow us to store user-specific data and maintain state across multiple page requests.

Cookies, on the other hand, are small pieces of data stored on the client-side, typically in the user's browser. They enable us to store and retrieve information about the user and maintain state persistently.

## Managing Sessions in Flutter SSR

To manage user sessions in a Flutter SSR application, we can make use of session middleware packages like `shelf_session` or `angel_sessions`.

These packages provide APIs to handle session creation, storage, and retrieval. They typically use cookies to store session IDs on the client and store session data on the server.

## Example: Using `shelf_session` package

1. Start by adding the `shelf_session` package to your `pubspec.yaml` file:

```yaml
dependencies:
  shelf_session: ^X.X.X
```

2. Import the necessary libraries in your Dart file:

```dart
import 'package:shelf/shelf.dart';
import 'package:shelf_session/shelf_session.dart';
```

3. Define a session handler by initializing a `SessionMiddleware`:

```dart
var sessionHandler = SessionMiddleware(
  CookieSessionStorage(Cookie('SESSION_NAME')),
);
```
Replace `'SESSION_NAME'` with a unique name for your session.

4. Use the session handler in your flutter_ssr `handleRequest` function:

```dart
var app = FlutterSsr(
  handleRequest: (request) async {
    var session = await sessionHandler.getSession(request);
    
    // Access session data
    var value = session['key'];
  
    // Modify session data
    session['key] = 'newValue';
  
    return Response.ok('Hello, $value!');
  },
);
```

Remember to replace `'key'` with the actual key you want to store or retrieve. Modify the session data as per your application needs.

## Managing Cookies in Flutter SSR

To manage cookies in a Flutter SSR application, we can use `dart:io` library which provides `Cookie` class to create, access, and manipulate cookies. 

## Example: Setting a Cookie

To set a cookie on the client-side, we need access to the `HttpResponse` object from the `shelf` package. Here's an example of setting a cookie in Flutter SSR using `shelf`:

```dart
var app = FlutterSsr(
  handleRequest: (request) async {
    var response = Response.ok('Hello, Flutter SSR!');
    
    var cookie = Cookie('COOKIE_NAME', 'cookieValue')
      ..path = '/' // set the path for which the cookie is valid
      ..expires = DateTime.now().add(Duration(days: 365)); // set an expiration date
    
    response = response.change(headers: {
      HttpHeaders.setCookieHeader: cookie.toString(),
    });
    
    return response;
  },
);
```

Remember to replace `'COOKIE_NAME'` and `'cookieValue'` with the actual cookie name and value.

## Conclusion

In this blog post, we learned how to handle user sessions and cookies in Flutter SSR applications. We explored how to manage sessions using libraries like `shelf_session` and how to manipulate cookies using `dart:io`. By leveraging these techniques, you can create stateful and personalized experiences for your users in your Flutter SSR applications.

#flutter #ssr