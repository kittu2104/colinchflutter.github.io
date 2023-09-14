---
layout: post
title: "Creating beautiful charts and graphs with Flutter widgets"
description: " "
date: 2023-09-14
tags: [flutter, charts]
comments: true
share: true
---

If you're building a mobile app that involves displaying data in a visually appealing way, **charts and graphs** can be a powerful tool. Flutter, Google's open-source UI toolkit, offers a variety of **widget libraries** that make it easy to create stunning charts and graphs.

In this article, we will explore some of the popular **Flutter widget libraries** for creating beautiful charts and graphs, and we will provide examples of how to use them in your Flutter app.

## 1. **charts_flutter** library

The **charts_flutter** library, developed by the Flutter team, provides a wide range of chart types, including **line charts**, **bar charts**, **pie charts**, and **scatter plots**. It supports both iOS and Android platforms and offers extensive customizability options.

To get started, first, add the `charts_flutter` library as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter

  charts_flutter: ^0.12.0
```

Once you have added the dependency, you can import the library in your Dart file:

```dart
import 'package:charts_flutter/flutter.dart' as charts;
```

Now you can create visually stunning charts and graphs using the various chart types provided by the library. Here's an example of creating a simple line chart:

```dart
class LineChartWidget extends StatelessWidget {

  final List<charts.Series<dynamic, int>> seriesList;
  final bool animate;

  LineChartWidget(this.seriesList, {this.animate});

  @override
  Widget build(BuildContext context) {
    return charts.LineChart(
      seriesList,
      animate: animate,
      defaultRenderer: charts.LineRendererConfig(includePoints: true),
    );
  }
}
```

## 2. **syncfusion_flutter_charts** library

Another popular Flutter charting library is the **syncfusion_flutter_charts** library by Syncfusion. It offers a wide range of chart types, including **line charts**, **area charts**, **bar charts**, and many more. It also provides various customization options and interactions like zooming and panning.

To get started, add the `syncfusion_flutter_charts` library as a dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  flutter:
    sdk: flutter

  syncfusion_flutter_charts: ^19.2.45
```

Now import the library in your Dart file:

```dart
import 'package:syncfusion_flutter_charts/charts.dart';
```

You can then create beautiful charts and graphs using the various chart types provided by the library. Here's an example of creating a simple bar chart:

```dart
class BarChartWidget extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return SfCartesianChart(
      primaryXAxis: CategoryAxis(),
      series: <ChartSeries>[
        ColumnSeries<MyData, String>(
          dataSource: <MyData>[
            MyData('Apple', 35),
            MyData('Orange', 64),
            MyData('Banana', 80),
            MyData('Mango', 55),
          ],
          xValueMapper: (MyData data, _) => data.category,
          yValueMapper: (MyData data, _) => data.value,
        ),
      ],
    );
  }
}

class MyData {
  final String category;
  final int value;

  MyData(this.category, this.value);
}
```

These are just two examples of Flutter libraries that can help you create beautiful charts and graphs in your app. Depending on your specific requirements and design preferences, you can choose the library that best fits your needs.

# Conclusion

Visualizing data using charts and graphs is a powerful way to communicate information in a mobile app. With Flutter, you have access to various libraries that make it easy to create visually appealing and interactive charts and graphs. Whether you choose the `charts_flutter` library or the `syncfusion_flutter_charts` library, you'll be able to create stunning visual representations of your data quickly and easily.

#flutter #charts