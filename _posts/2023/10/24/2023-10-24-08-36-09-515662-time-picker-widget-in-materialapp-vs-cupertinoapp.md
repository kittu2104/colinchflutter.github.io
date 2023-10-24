---
layout: post
title: "Time picker widget in MaterialApp vs CupertinoApp"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

When developing a mobile app using Flutter, you have the choice between MaterialApp and CupertinoApp as the base for your application's design. Each framework comes with its own set of UI widgets that adhere to the platform-specific design guidelines - Material Design for MaterialApp and Apple's Human Interface Guidelines for CupertinoApp.

In this blog post, we will compare and discuss the time picker widget available in MaterialApp and CupertinoApp, and highlight the differences between the two.

## MaterialApp Time Picker

The Material Design time picker widget in MaterialApp is based on the TimePicker widget provided by the Flutter framework. It allows you to select a specific time using a dialog-style interface with hours and minutes selectors.

To use the Material Design time picker, you can simply include it in your widget tree using the `showTimePicker` function. For example:

```dart
showTimePicker(
  context: context,
  initialTime: TimeOfDay.now(),
).then((selectedTime) {
  if (selectedTime != null) {
    print('Selected time: ${selectedTime.format(context)}');
  }
});
```

In the above code snippet, `showTimePicker` function is called to display the time picker dialog. The `context` parameter is required and the `initialTime` parameter sets the initial time value. The `then` method allows you to handle the selected time when the dialog is closed.

## CupertinoApp Time Picker

The CupertinoApp framework, on the other hand, provides a time picker widget that is styled according to the iOS design guidelines. The CupertinoDatePicker widget can be used to select a time in a native iOS-like manner.

To use the Cupertino time picker, you can include the CupertinoDatePicker widget in your widget tree. For example:

```dart
CupertinoDatePicker(
  mode: CupertinoDatePickerMode.time,
  initialDateTime: DateTime.now(),
  onDateTimeChanged: (selectedTime) {
    print('Selected time: $selectedTime');
  },
)
```

In the above code snippet, the `mode` parameter is set to `CupertinoDatePickerMode.time` to indicate that we are only interested in selecting time. The `initialDateTime` parameter sets the initial time value, and the `onDateTimeChanged` callback function is called whenever the selected time changes.

## Differences and Considerations

The main difference between the time picker in MaterialApp and CupertinoApp is their visual appearance and adherence to respective platform design guidelines. MaterialApp uses Material Design elements and provides a dialog-style interface, while CupertinoApp imitates the iOS look and feel with a native-like picker.

When choosing between the two time pickers, it is important to consider the overall design and user experience of your application. If your app targets both Android and iOS, MaterialApp may provide a consistent design across platforms. However, if your app is exclusively for iOS users or you want to match the iOS design closely, then the CupertinoApp time picker may be a better choice.

## Conclusion

In this blog post, we compared the time picker widget available in MaterialApp and CupertinoApp for Flutter. We discussed how to use each time picker widget and highlighted the differences between the two. Depending on your app's design requirements and target platform, you can choose between MaterialApp's Material Design time picker or CupertinoApp's iOS-style time picker.