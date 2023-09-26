---
layout: post
title: "How to parse XML responses using the http package in Flutter?"
description: " "
date: 2023-09-27
tags: []
comments: true
share: true
---

When working with APIs in Flutter, we often receive XML responses that need to be parsed to extract the desired information. In this blog post, we will explore how to parse XML responses using the `http` package in Flutter.

## Prerequisites
Before we start, make sure you have the `http` package added to your `pubspec.yaml` file:

```yaml
dependencies:
  http: ^0.13.4
```

## Making an API request
To make an API request and receive an XML response, we can use the `get` method from the `http` package. Here's an example:

```dart
import 'package:http/http.dart' as http;

Future<void> fetchXMLData() async {
  final response = await http.get(Uri.parse('https://example.com/api'));

  if (response.statusCode == 200) {
    // Parse the XML response here
  } else {
    // Handle API error
    print('API request failed with ${response.statusCode}');
  }
}
```

## Parsing XML Response
To parse the XML response, we can make use of the `xml` package, which is also provided by Dart. Add the following import statement at the top of your file:

```dart
import 'package:xml/xml.dart' as xml;
```

Next, we can create an `XmlDocument` object by parsing the response body. Here's an example:

```dart
final xmlDoc = xml.XmlDocument.parse(response.body);
```

Now that we have the parsed XML document, we can navigate through the XML structure and extract the desired information using XPath expressions. The `xml` package provides a rich set of APIs for this purpose. Let's say we have an XML response like this:

```xml
<root>
  <item>
    <name>Item 1</name>
    <price>10</price>
  </item>
  <item>
    <name>Item 2</name>
    <price>20</price>
  </item>
</root>
```

We can extract the names of all the items using the following code:

```dart
final itemNodes = xmlDoc.findAllElements('item');
final itemNames = itemNodes.map((node) => node.findElements('name').single.text).toList();

print(itemNames); // Output: [Item 1, Item 2]
```

## Summary
In this tutorial, we learned how to parse XML responses using the `http` package in Flutter. We made an API request and received an XML response. Then, we used the `xml` package to parse the XML document and extract the desired information using XPath expressions.

Make sure to handle any errors that might occur during the API request or XML parsing process.