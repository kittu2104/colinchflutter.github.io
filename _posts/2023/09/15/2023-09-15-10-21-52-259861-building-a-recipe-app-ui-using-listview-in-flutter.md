---
layout: post
title: "Building a recipe app UI using ListView in Flutter."
description: " "
date: 2023-09-15
tags: [recipeapp]
comments: true
share: true
---

In this tutorial, we will explore how to build a recipe app UI using the ListView widget in Flutter. ListView is a commonly used widget in Flutter for creating scrollable lists of items.

## Prerequisites

Before getting started, make sure you have Flutter installed on your machine. You can follow the [official Flutter installation guide](https://flutter.dev/docs/get-started/install) to set up Flutter on your system.

## Step 1: Setting up the Flutter project

First, let's create a new Flutter project by executing the following command in your terminal:

```shell
flutter create recipe_app
```

Navigate into the project directory:

```shell
cd recipe_app
```

## Step 2: Creating the recipe model

Next, let's create a recipe model that will represent the data for our recipe app. Create a new file called `recipe_model.dart` in the `lib` folder and add the following code:

```dart
class Recipe {
  final String title;
  final String description;
  final String imageUrl;

  Recipe({required this.title, required this.description, required this.imageUrl});
}
```

## Step 3: Building the recipe list UI

In the `lib` folder, open the `main.dart` file and replace the existing code with the following:

```dart
import 'package:flutter/material.dart';
import 'recipe_model.dart';

void main() {
  runApp(RecipeApp());
}

class RecipeApp extends StatelessWidget {
  final List<Recipe> recipes = [
    Recipe(
      title: 'Chocolate Cake',
      description: 'A delicious and moist chocolate cake.',
      imageUrl: 'https://example.com/chocolate_cake.jpg',
    ),
    Recipe(
      title: 'Pasta Carbonara',
      description: 'An Italian classic pasta dish with eggs and bacon.',
      imageUrl: 'https://example.com/pasta_carbonara.jpg',
    ),
    // Add more recipe items as needed
  ];

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Recipe App'),
        ),
        body: ListView.builder(
          itemCount: recipes.length,
          itemBuilder: (context, index) {
            return ListTile(
              leading: Image.network(recipes[index].imageUrl),
              title: Text(recipes[index].title),
              subtitle: Text(recipes[index].description),
            );
          },
        ),
      ),
    );
  }
}
```

In this code, we have defined a `RecipeApp` widget that displays a `ListView.builder`. The `ListView.builder` dynamically generates `ListTile` widgets based on the number of recipes in the `recipes` list.

## Step 4: Running the app

Save the changes and run the app with the following command:

```shell
flutter run
```

You should now see a recipe app UI with a scrollable list of recipe items. Each item displays the image, title, and description of the recipe.

## Conclusion

In this tutorial, we learned how to build a recipe app UI using the ListView widget in Flutter. The ListView widget allows us to create dynamic and scrollable lists of items easily. You can further enhance the app by adding more features, such as navigation to a recipe details page or filtering the recipes based on categories.

#flutter #recipeapp