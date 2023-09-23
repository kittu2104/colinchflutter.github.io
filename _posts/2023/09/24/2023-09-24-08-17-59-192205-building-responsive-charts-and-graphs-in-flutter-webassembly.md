---
layout: post
title: "Building responsive charts and graphs in Flutter WebAssembly"
description: " "
date: 2023-09-24
tags: [flutter, webassembly]
comments: true
share: true
---

With the rise of web development using WebAssembly, Flutter has become one of the most popular frameworks for building responsive and interactive user interfaces. In this tutorial, we will explore how to build responsive charts and graphs using Flutter WebAssembly.

## Why Use Flutter WebAssembly for Charts and Graphs?

Flutter WebAssembly provides a high-performance and cross-platform solution for building charts and graphs. It allows developers to leverage the power of Flutter's rich set of UI components and the flexibility of web technologies.

## Getting Started

To get started, make sure you have Flutter SDK and WebAssembly tooling installed on your machine. You can find detailed instructions for setting up Flutter WebAssembly in the official Flutter documentation.

## Charting Library

For this tutorial, we will use the `charts_flutter` library, which is a powerful Flutter library for creating charts and graphs. To add the library to your project, add the following dependency in your `pubspec.yaml` file:

```dart
dependencies:
  charts_flutter: ^1.1.0
```

After adding the dependency, run `flutter pub get` to download and install the package.

## Creating a Simple Bar Chart

Let's start by creating a simple bar chart. Create a new Flutter widget and import the necessary libraries:

```dart
import 'package:charts_flutter/flutter.dart' as charts;
import 'package:flutter/material.dart';
```

Define a class for the data that will be used to populate the chart:

```dart
class ChartData {
  final String label;
  final int value;

  ChartData(this.label, this.value);
}
```

Next, create a list of data points:

```dart
final List<ChartData> data = [
  ChartData('Label 1', 10),
  ChartData('Label 2', 20),
  ChartData('Label 3', 15),
];
```

Create a `charts.Series` with the data and chart type:

```dart
final series = [
  charts.Series(
    id: 'Data',
    data: data,
    domainFn: (ChartData chartData, _) => chartData.label,
    measureFn: (ChartData chartData, _) => chartData.value,
  )
];
```

Create a `charts.BarChart` widget to display the bar chart:

```dart
final chart = charts.BarChart(
  series,
  animate: true,
);
```

Finally, wrap the chart in a `Scaffold` widget and display it:

```dart
class ChartScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Bar Chart'),
      ),
      body: Center(
        child: chart,
      ),
    );
  }
}
```

## Making the Chart Responsive

To make the chart responsive, we can use Flutter's `LayoutBuilder` widget. Wrap the `BarChart` widget with a `LayoutBuilder` and use the available constraints to calculate the size of the chart:

```dart
final chart = charts.BarChart(
  series,
  animate: true,
  defaultRenderer: charts.BarRendererConfig(
    groupingType: charts.BarGroupingType.grouped,
    strokeWidthPx: 0,
  ),
  domainAxis: charts.OrdinalAxisSpec(renderSpec: charts.NoneRenderSpec()),
  primaryMeasureAxis: charts.NumericAxisSpec(renderSpec: charts.NoneRenderSpec()),
  layoutConfig: charts.LayoutConfig(
    leftMarginSpec: charts.MarginSpec.fromPixelValue(0),
    topMarginSpec: charts.MarginSpec.fromPixelValue(0),
    rightMarginSpec: charts.MarginSpec.fromPixelValue(0),
    bottomMarginSpec: charts.MarginSpec.fromPixelValue(0),
  ),
  behaviors: [
    charts.LayoutAutoAdjustment(),
  ],
);
```

By using `LayoutBuilder`, the chart will automatically adjust its size to fit the available space.

## Conclusion

In this tutorial, we explored how to build responsive charts and graphs using Flutter WebAssembly. We used the `charts_flutter` library to create a simple bar chart and made it responsive using Flutter's `LayoutBuilder` widget.

Flutter WebAssembly provides a flexible and high-performance solution for creating interactive and visually appealing charts and graphs. With the power of Flutter and web technologies, you can easily customize and enhance your charts to suit your application's needs.

#flutter #webassembly