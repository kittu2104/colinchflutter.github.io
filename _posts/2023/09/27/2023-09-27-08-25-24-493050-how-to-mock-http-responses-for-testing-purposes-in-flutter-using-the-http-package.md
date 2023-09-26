---
layout: post
title: "How to mock http responses for testing purposes in Flutter using the http package?"
description: " "
date: 2023-09-27
tags: [testing]
comments: true
share: true
---

When testing Flutter applications, it is common to mock HTTP responses to simulate different scenarios and ensure that the app behaves correctly. This can be done using the `http` package along with a testing library like `mockito`. In this blog post, you will learn how to mock HTTP responses in Flutter using the `http` package.

## Step 1: Add the `http` and `mockito` packages to your project

To get started, open your project's `pubspec.yaml` file and add the `http` and `mockito` packages as dependencies:

```yaml
dev_dependencies:
  http: ^0.13.3
  mockito: ^5.0.11
```

Save the file and run `flutter pub get` to fetch the packages.

## Step 2: Mock the HTTP responses

Next, create a new test file (e.g., `http_mock_test.dart`) for your tests. Import the necessary packages and define your test case:

```dart
import 'package:http/http.dart' as http;
import 'package:flutter_test/flutter_test.dart';
import 'package:mockito/annotations.dart';
import 'package:mockito/mockito.dart';

class MockClient extends Mock implements http.Client {}

@GenerateMocks([http.Response])
void main() {
  group('MyAPI', () {
    late MockClient mockClient;
    late MyAPI api;

    final mockedResponse = http.Response('Mocked response body', 200);

    setUp(() {
      mockClient = MockClient();
      api = MyAPI(client: mockClient);
    });

    test('fetchData should return mocked response', () async {
      when(mockClient.get(Uri.parse('https://api.example.com/data')))
          .thenAnswer((_) async => mockedResponse);

      final result = await api.fetchData();

      expect(result, 'Mocked response body');
    });
  });
}
```

In the above code, we create a `MockClient` class that extends `Mock` from the `mockito` package. We also generate a mock class for `http.Response` using the `@GenerateMocks` annotation.

Inside the test case, we initialize the mock client and the API instance. We define the mocked response using the `http.Response` class and `when..thenAnswer` to specify the response when `mockClient.get` is called.

Finally, we call the API method (`fetchData` in this example) and assert that the result matches the expected mocked response.

## Step 3: Run the tests

To run the tests, use the Flutter test command:

```bash
flutter test
```

The tests should execute, and you should see the test results in the console.

## Conclusion

Mocking HTTP responses is essential for testing Flutter applications, as it allows you to simulate various scenarios and ensure your app behaves correctly. By using the `http` package and `mockito`, you can easily mock HTTP responses in your Flutter tests. This helps you create reliable and robust tests for your app.

#flutter #testing