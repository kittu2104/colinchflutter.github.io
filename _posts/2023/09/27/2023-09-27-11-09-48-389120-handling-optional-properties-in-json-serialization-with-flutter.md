---
layout: post
title: "Handling optional properties in JSON serialization with Flutter"
description: " "
date: 2023-09-27
tags: [JSONSerialization]
comments: true
share: true
---

JSON (JavaScript Object Notation) is a widely used format for data interchange. When working with APIs or networking in Flutter, you often need to parse JSON responses into Dart objects. In many cases, the JSON response may contain optional properties that may or may not be present.

In this blog post, we will explore how to handle optional properties in JSON serialization with Flutter using the `json_serializable` package.

## Setting up the project

Before we dive into the implementation details, let's set up a new Flutter project and include the necessary dependencies.

1. Create a new Flutter project:

   ```bash
   flutter create json_serialization_example
   ```

2. Open your project in an IDE of your choice and add the following dependencies to your `pubspec.yaml` file:

   ```yaml
   dependencies:
     flutter:
       sdk: flutter
     json_annotation: ^4.3.0
     json_serializable: ^4.1.4
   ```

   Run `flutter packages get` to fetch the dependencies.

## Creating the model class

Let's assume we have a simple JSON response that represents a user's profile, which may or may not contain an optional property called `bio`.

```json
{
  "name": "John Doe",
  "age": 25,
  "bio": "Lorem ipsum dolor sit amet"
}
```

We can define a Dart model class representing this JSON structure with the optional `bio` property.

```dart
import 'package:json_annotation/json_annotation.dart';

part 'user_profile.g.dart';

@JsonSerializable()
class UserProfile {
  final String name;
  final int age;
  final String? bio; // Optional property

  UserProfile({
    required this.name,
    required this.age,
    this.bio,
  });

  factory UserProfile.fromJson(Map<String, dynamic> json) =>
      _$UserProfileFromJson(json);

  Map<String, dynamic> toJson() => _$UserProfileToJson(this);
}
```

Note the use of the `?` symbol in the type declaration `String? bio`. This denotes that the `bio` property is optional and can be `null` in Dart.

## Generating serialization code

To enable JSON serialization, we need to generate the serialization code for our model class. This can be done automatically using the `json_serializable` package.

1. Run the following command in the terminal:

   ```bash
   flutter pub run build_runner build
   ```

   This generates the necessary serialization code for your model class.

2. After running the command, you will see a new file named `user_profile.g.dart` next to your `user_profile.dart` file. Do not modify this generated file as it will be overwritten every time you run the build command.

## Using the model class

Now that we have our model class set up, let's see how we can use it to parse JSON responses.

```dart
import 'dart:convert';

void main() {
  String jsonStr = '''
    {
      "name": "John Doe",
      "age": 25,
      "bio": "Lorem ipsum dolor sit amet"
    }
  ''';

  Map<String, dynamic> json = jsonDecode(jsonStr);
  UserProfile userProfile = UserProfile.fromJson(json);

  print('Name: ${userProfile.name}');
  print('Age: ${userProfile.age}');
  if (userProfile.bio != null) {
    print('Bio: ${userProfile.bio}');
  } else {
    print('Bio is not available');
  }
}
```

In the above code, we decode the JSON string using `jsonDecode` from the `dart:convert` library. Then we create an instance of `UserProfile` using the `fromJson` factory method. Finally, we can access the properties of the `userProfile` object, checking for the presence of the optional `bio` property.

## Conclusion

Handling optional properties in JSON serialization with Flutter can be easily done using the `json_serializable` package. By defining our model class with optional properties and generating the necessary serialization code, we can seamlessly parse JSON responses that may or may not contain certain properties.

Remember to always handle optional properties with care and account for the cases where they may be null. This will ensure robustness and prevent runtime crashes in your app.

Happy coding!

------------------------------

\#Flutter #JSONSerialization