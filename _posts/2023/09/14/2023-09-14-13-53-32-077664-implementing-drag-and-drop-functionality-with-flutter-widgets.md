---
layout: post
title: "Implementing drag and drop functionality with Flutter widgets"
description: " "
date: 2023-09-14
tags: [dart]
comments: true
share: true
---

Flutter is a popular cross-platform framework for building mobile applications. It provides a rich set of widgets that can be used to create interactive and engaging user interfaces. One of the common requirements in mobile app development is to implement drag and drop functionality, where users can move objects around the screen. In this blog post, we will explore how to implement drag and drop functionality with Flutter widgets.

## The DragTarget Widget

Flutter provides the `DragTarget` widget, which is used to define a widget that can accept a dragged item. To implement drag and drop functionality, we need to wrap the widget that should accept the dragged item with a `DragTarget`. The `DragTarget` widget takes a generic type parameter that represents the type of the data that can be dropped onto it.

```dart
DragTarget<T>(
  builder: (
    BuildContext context,
    List<T> candidateData,
    List<dynamic> rejectedData,
  ) {
    // Return the widget that will be displayed when the item is dragged over
    return Container(
      // Define the appearance of the drop target
      color: Colors.blue,
      width: 200,
      height: 200,
      child: Center(
        child: Text("Drop here"),
      ),
    );
  },
  onAccept: (T data) {
    // Perform necessary actions when the item is dropped onto the target
    // Here you can update the state or perform any other logic specific to your app
    // For example, you can add the dropped item to a list of items
    // or display a message to the user indicating the successful drop.
  },
)
```

In the above code snippet, we define a `DragTarget` widget that accepts data of type `T`. The `builder` function is responsible for defining the appearance of the drop target. In this example, we display a container with blue background color and text that says "Drop here". The `onAccept` callback is triggered when an item is dropped onto the target. Inside this callback, you can handle the logic specific to your application, such as updating the state or performing any other actions.

## The Draggable Widget

To enable an item to be dragged, we need to wrap it with the `Draggable` widget. The `Draggable` widget also takes a generic type parameter that specifies the type of the data being dragged.

```dart
Draggable<T>(
  data: myData, // Specify the data that will be passed when the item is dropped onto the target
  child: Container(
    // Define the appearance of the draggable item
    color: Colors.red,
    width: 100,
    height: 100,
    child: Center(
      child: Text("Drag me"),
    ),
  ),
  feedback: Container(
    // Define the appearance of the dragged item
    color: Colors.red.withOpacity(0.5),
    width: 100,
    height: 100,
    child: Center(
      child: Text("Dragging..."),
    ),
  ),
)
```

In the code snippet above, we wrap a `Container` with the `Draggable` widget. Inside the `Draggable` widget, we define the appearance of the draggable item using the `child` property. We also specify the data that will be passed when the item is dropped onto the target using the `data` property. The `feedback` property is used to define the appearance of the dragged item that is displayed while dragging. In this example, we display a slightly transparent container with the text "Dragging..." when the item is being dragged.

## Putting it all together

To implement drag and drop functionality, we need to combine the `DragTarget` and `Draggable` widgets. Here's an example that demonstrates how to implement a basic drag and drop functionality in Flutter:

```dart
class DragAndDropExample extends StatefulWidget {
  @override
  _DragAndDropExampleState createState() => _DragAndDropExampleState();
}

class _DragAndDropExampleState extends State<DragAndDropExample> {
  List<String> items = ['Item 1', 'Item 2', 'Item 3'];

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("Drag and Drop Example"),
      ),
      body: Column(
        children: [
          DragTarget<String>(
            builder: (
              BuildContext context,
              List<String> candidateData,
              List<dynamic> rejectedData,
            ) {
              return Container(
                color: Colors.blue,
                width: 200,
                height: 200,
                child: Center(
                  child: Text("Drop here"),
                ),
              );
            },
            onAccept: (String data) {
              setState(() {
                items.add(data);
              });
            },
          ),
          SizedBox(height: 20),
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: [
              Draggable<String>(
                data: 'Item 1',
                child: Container(
                  color: Colors.red,
                  width: 100,
                  height: 100,
                  child: Center(
                    child: Text("Item 1"),
                  ),
                ),
                feedback: Container(
                  color: Colors.red.withOpacity(0.5),
                  width: 100,
                  height: 100,
                  child: Center(
                    child: Text("Dragging..."),
                  ),
                ),
              ),
              Draggable<String>(
                data: 'Item 2',
                child: Container(
                  color: Colors.green,
                  width: 100,
                  height: 100,
                  child: Center(
                    child: Text("Item 2"),
                  ),
                ),
                feedback: Container(
                  color: Colors.green.withOpacity(0.5),
                  width: 100,
                  height: 100,
                  child: Center(
                    child: Text("Dragging..."),
                  ),
                ),
              ),
              Draggable<String>(
                data: 'Item 3',
                child: Container(
                  color: Colors.yellow,
                  width: 100,
                  height: 100,
                  child: Center(
                    child: Text("Item 3"),
                  ),
                ),
                feedback: Container(
                  color: Colors.yellow.withOpacity(0.5),
                  width: 100,
                  height: 100,
                  child: Center(
                    child: Text("Dragging..."),
                  ),
                ),
              ),
            ],
          ),
          SizedBox(height: 20),
          Text('Dropped Items:'),
          SizedBox(height: 10),
          ListView.builder(
            itemCount: items.length,
            itemBuilder: (context, index) {
              return ListTile(title: Text(items[index]));
            },
          ),
        ],
      ),
    );
  }
}
```

In this example, we create a `DragAndDropExample` widget that contains a `DragTarget` at the top, followed by draggable items wrapped inside a `Row`. We maintain a list of dropped items in the `_DragAndDropExampleState` using the `items` list. Whenever an item is dropped onto the target, the `onAccept` callback is triggered, and we update the state to add the dropped item to the list. Lastly, we display the dropped items using a `ListView.builder`.

By combining the `DragTarget` and `Draggable` widgets, we can easily implement drag and drop functionality in Flutter. This allows users to interact with the app in a more intuitive and engaging manner.

#flutter #dart