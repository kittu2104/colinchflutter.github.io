---
layout: post
title: "Implementing autoboxing and unboxing using Java wrapper classes"
description: " "
date: 2023-09-14
tags: []
comments: true
share: true
---

Autoboxing and unboxing are convenient features in Java that allow automatic conversion between primitive types and their corresponding wrapper classes. This makes it easier to work with both primitive types and objects in a seamless manner.

Autoboxing: The process of converting a primitive type to its corresponding wrapper class.
Unboxing: The process of converting a wrapper class object to its corresponding primitive type.

In Java, there are wrapper classes for each primitive type: `Integer` for `int`, `Double` for `double`, `Boolean` for `boolean`, and so on.

## Autoboxing Example:

Autoboxing allows you to assign a primitive value to its corresponding wrapper class without explicitly creating an object.

```java
int num = 10; // primitive int
Integer wrappedNum = num; // autoboxing: primitive int to Integer object

System.out.println(wrappedNum); // Output: 10
```

Here, the value of `num` is automatically boxed into an `Integer` object when assigned to `wrappedNum`.

## Unboxing Example:

Unboxing allows you to extract the primitive value from a wrapper class object.

```java
Integer wrappedNum = 20; // Integer object
int num = wrappedNum; // unboxing: Integer object to primitive int

System.out.println(num); // Output: 20
```

In this example, the value of `wrappedNum` is automatically unboxed and assigned to `num`.

Using autoboxing and unboxing, you can seamlessly switch between primitive types and their corresponding wrapper classes, making the code more readable and easier to maintain.

## Conclusion:

Autoboxing and unboxing using Java wrapper classes provide a convenient way to work with primitive types and objects interchangeably. These features eliminate the need for manual conversions and improve code readability. It is important, however, to keep in mind the potential impact on performance when working with large amounts of data.