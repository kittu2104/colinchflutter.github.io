---
layout: post
title: "Flutter radio button state management"
description: " "
date: 2023-10-10
tags: [radiobuttons]
comments: true
share: true
---

Radio buttons in Flutter are a commonly used UI element for selecting a single option from a set of choices. However, managing the state of radio buttons can be a bit tricky if not implemented correctly.

In this blog post, we will explore different approaches to manage the state of radio buttons in Flutter.

## Table of Contents
- [Local State Management](#local-state-management)
- [State Management with Provider](#state-management-with-provider)
- [State Management with BLoC](#state-management-with-bloc)

## Local State Management

The simplest way to manage the state of radio buttons is by using local state within the widget itself. We can achieve this by maintaining a selected option variable and updating its value whenever a radio button is selected. Here is an example:

```dart
class RadioButtonExample extends StatefulWidget {
  @override
  _RadioButtonExampleState createState() => _RadioButtonExampleState();
}

class _RadioButtonExampleState extends State<RadioButtonExample> {
  String selectedOption;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: <Widget>[
        RadioListTile(
          value: 'Option 1',
          groupValue: selectedOption,
          onChanged: (value) {
            setState(() {
              selectedOption = value;
            });
          },
          title: Text('Option 1'),
        ),
        RadioListTile(
          value: 'Option 2',
          groupValue: selectedOption,
          onChanged: (value) {
            setState(() {
              selectedOption = value;
            });
          },
          title: Text('Option 2'),
        ),
        RadioListTile(
          value: 'Option 3',
          groupValue: selectedOption,
          onChanged: (value) {
            setState(() {
              selectedOption = value;
            });
          },
          title: Text('Option 3'),
        ),
      ],
    );
  }
}
```

In this example, we maintain a `selectedOption` variable which holds the currently selected option. Each radio button has an `onChanged` callback that updates the `selectedOption` value when it is selected.

## State Management with Provider

To manage the state of radio buttons globally across multiple screens, we can use a state management solution like Provider. Provider allows us to create a data model that can be accessed and updated from any widget in the widget tree.

Here's an example using the `provider` package:

```dart
class RadioModel extends ChangeNotifier {
  String _selectedOption;

  String get selectedOption => _selectedOption;

  void setSelectedOption(String option) {
    _selectedOption = option;
    notifyListeners();
  }
}

class RadioButtonExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Consumer<RadioModel>(
      builder: (context, radioModel, _) {
        return Column(
          children: <Widget>[
            RadioListTile(
              value: 'Option 1',
              groupValue: radioModel.selectedOption,
              onChanged: (value) {
                radioModel.setSelectedOption(value);
              },
              title: Text('Option 1'),
            ),
            RadioListTile(
              value: 'Option 2',
              groupValue: radioModel.selectedOption,
              onChanged: (value) {
                radioModel.setSelectedOption(value);
              },
              title: Text('Option 2'),
            ),
            RadioListTile(
              value: 'Option 3',
              groupValue: radioModel.selectedOption,
              onChanged: (value) {
                radioModel.setSelectedOption(value);
              },
              title: Text('Option 3'),
            ),
          ],
        );
      },
    );
  }
}
```

In this example, we create a `RadioModel` class that extends `ChangeNotifier`. It has a `selectedOption` property and a `setSelectedOption` method that updates the selected option and notifies the listeners. We wrap the radio buttons widget in a `Consumer` that rebuilds whenever the `RadioModel` data changes.

## State Management with BLoC

Another approach to managing the state of radio buttons is by using the BLoC (Business Logic Component) pattern. BLoC separates the business logic and UI, making it easier to manage the state and handle events.

Here's an example using the `flutter_bloc` package:

```dart
enum RadioButtonEvent {
  option1Selected,
  option2Selected,
  option3Selected,
}

class RadioButtonBloc extends Bloc<RadioButtonEvent, String> {
  @override
  String get initialState => 'Option 1';

  @override
  Stream<String> mapEventToState(RadioButtonEvent event) async* {
    switch (event) {
      case RadioButtonEvent.option1Selected:
        yield 'Option 1';
        break;
      case RadioButtonEvent.option2Selected:
        yield 'Option 2';
        break;
      case RadioButtonEvent.option3Selected:
        yield 'Option 3';
        break;
    }
  }
}

class RadioButtonExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocBuilder<RadioButtonBloc, String>(
      builder: (context, selectedOption) {
        return Column(
          children: <Widget>[
            RadioListTile(
              value: 'Option 1',
              groupValue: selectedOption,
              onChanged: (_) {
                context.read<RadioButtonBloc>().add(RadioButtonEvent.option1Selected);
              },
              title: Text('Option 1'),
            ),
            RadioListTile(
              value: 'Option 2',
              groupValue: selectedOption,
              onChanged: (_) {
                context.read<RadioButtonBloc>().add(RadioButtonEvent.option2Selected);
              },
              title: Text('Option 2'),
            ),
            RadioListTile(
              value: 'Option 3',
              groupValue: selectedOption,
              onChanged: (_) {
                context.read<RadioButtonBloc>().add(RadioButtonEvent.option3Selected);
              },
              title: Text('Option 3'),
            ),
          ],
        );
      },
    );
  }
}
```

In this example, we define a `RadioButtonEvent` enum that represents different events that can occur. We create a `RadioButtonBloc` class that extends `Bloc` and handles these events. The `mapEventToState` method maps the events to the new state. We use `BlocBuilder` to rebuild the widget whenever the state of the bloc changes.

## Conclusion

Managing the state of radio buttons in Flutter can be approached in multiple ways, depending on the complexity and scope of your application. The choice between local state management, Provider, or BLoC depends on the specific requirements of your project.

Using local state management is suitable for simple cases where the state is limited to a single widget. Provider is a good choice when you need to share the state between multiple screens. BLoC pattern offers more flexibility and separation of concerns for complex state management scenarios.

Choose the approach that best suits your needs and enhances the user experience of your Flutter application.

#flutter #radiobuttons