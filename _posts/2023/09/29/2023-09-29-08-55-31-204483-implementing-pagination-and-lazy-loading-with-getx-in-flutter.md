---
layout: post
title: "Implementing pagination and lazy loading with GetX in Flutter"
description: " "
date: 2023-09-29
tags: [Flutter, GetX]
comments: true
share: true
---

When building Flutter applications, it is common to display a large amount of data that needs to be paginated to enhance user experience and optimize resource consumption. Additionally, incorporating lazy loading allows for more efficient data retrieval and rendering. In this tutorial, we will explore how to implement pagination and lazy loading using GetX state management library in Flutter.

### What is GetX?

GetX is a powerful package for state management, dependency injection, and routing in Flutter. It provides a simple and intuitive way to handle state changes within your application. To get started, add the following dependency to your `pubspec.yaml` file:

```yaml
dependencies:
  get: ^4.1.4
```

### Setting up the Project

To begin, create a new Flutter project or open an existing one. Then, import the required packages:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
```

### Creating a Pagination Controller

The first step is to create a `PaginationController` that will handle the logic for pagination and lazy loading. This controller will keep track of the current page and fetch new data when necessary. Create a new file called `pagination_controller.dart` and add the following code:

```dart
import 'package:get/get.dart';

class PaginationController extends GetxController {
  final items = <String>[].obs;
  final isLoading = false.obs;
  final currentPage = 1.obs;

  @override
  void onInit() {
    super.onInit();
    fetchData();
  }

  Future<void> fetchData() async {
    try {
      isLoading.value = true;
      // Simulate network delay
      await Future.delayed(Duration(seconds: 2));

      // Fetch data for the current page
      final newData = List<String>.generate(10, (index) => 'Item ${index + 1}');
      items.addAll(newData);

      // Increment current page
      currentPage.value++;
    } finally {
      isLoading.value = false;
    }
  }
}
```

In the above code, we define three observables: `items` to store the fetched data, `isLoading` to indicate if new data is being fetched, and `currentPage` to keep track of the current page. In the `fetchData` method, we simulate a network delay using `Future.delayed`, fetch the data for the current page, and update the `items` list and `currentPage` value accordingly.

### Implementing the User Interface

Next, let's create a simple user interface to display the paginated data. In your main screen widget, add the following code:

```dart
import 'package:flutter/material.dart';
import 'package:get/get.dart';
import 'package:your_app_name/pagination_controller.dart';

class HomeScreen extends StatelessWidget {
  final controller = Get.put(PaginationController());

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Pagination Demo'),
      ),
      body: Obx(() {
        if (controller.isLoading.value && controller.items.isEmpty) {
          return Center(child: CircularProgressIndicator());
        } else if (controller.items.isEmpty) {
          return Center(child: Text('No items found'));
        } else {
          return ListView.builder(
            itemCount: controller.items.length + 1,
            itemBuilder: (context, index) {
              if (index == controller.items.length) {
                if (controller.isLoading.value) {
                  return Center(child: CircularProgressIndicator());
                } else {
                  return ElevatedButton(
                    onPressed: () => controller.fetchData(),
                    child: Text('Load More'),
                  );
                }
              } else {
                final item = controller.items[index];
                return ListTile(title: Text(item));
              }
            },
          );
        }
      }),
    );
  }
}
```

In the code above, we use the `Obx` widget from GetX to reactively update the UI whenever the observables in the `PaginationController` change. If the data is still loading and no items have been fetched yet, we display a circular progress indicator. If no items are present, we show a message indicating that no items were found. Otherwise, we display the items using a `ListView.builder`. When the last item in the list is reached, we show a "Load More" button if the data is not currently being fetched. When the button is pressed, we call the `fetchData` method to load more data.

### Wrapping up

With GetX and the `PaginationController`, you can easily implement pagination and lazy loading in your Flutter application. By handling state management and UI updates in a reactive manner, you can provide a seamless user experience while efficiently handling large datasets. Experiment with different configurations and enhancements to further improve the performance and user experience of your application.

Hashtags: #Flutter #GetX