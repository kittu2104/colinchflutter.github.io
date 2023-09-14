---
layout: post
title: "Implementing custom data structures using Java wrapper classes"
description: " "
date: 2023-09-14
tags: [customdatastructures, javawrappers]
comments: true
share: true
---

In Java, we often use the built-in data structures provided by the Java Collections Framework, such as List, Set, and Map. However, there may be times when we need to create custom data structures to better suit our specific needs. 

In this blog post, we will explore how to implement custom data structures using Java wrapper classes. These wrapper classes provide a convenient way to encapsulate our data and define custom behaviors.

## What are Wrapper Classes?

Wrapper classes in Java provide a way to convert primitive data types into objects. They are used to represent primitive data types as objects so that they can be used in collections, passed as parameters to methods that expect objects, and to perform various utility operations.

Some common wrapper classes include Integer, Double, Boolean, etc. These classes provide methods and constructors to work with the wrapped data effectively.

## Implementing a Custom Stack

Let's start by implementing a custom stack using a wrapper class in Java. A stack is a data structure that follows the Last-In-First-Out (LIFO) principle.

```java
public class CustomStack<T> {
    private List<T> stack;
    
    public CustomStack() {
        stack = new ArrayList<>();
    }
    
    public void push(T element) {
        stack.add(element);
    }
    
    public T pop() {
        if (isEmpty()) {
            throw new EmptyStackException();
        }
        return stack.remove(stack.size() - 1);
    }
    
    public T peek() {
        if (isEmpty()) {
            throw new EmptyStackException();
        }
        return stack.get(stack.size() - 1);
    }
    
    public boolean isEmpty() {
        return stack.isEmpty();
    }
    
    public int size() {
        return stack.size();
    }
}
```

In the above code, we have implemented a generic custom stack class using a Java wrapper class ArrayList. The `push` method adds an element to the top of the stack, while the `pop` method removes and returns the top element. The `peek` method returns the top element without removing it. The `isEmpty` method checks if the stack is empty, and the `size` method returns the current size of the stack.

## Implementing a Custom Queue

Now, let's implement a custom queue using a wrapper class in Java. A queue is a data structure that follows the First-In-First-Out (FIFO) principle.

```java
public class CustomQueue<T> {
    private List<T> queue;
    
    public CustomQueue() {
        queue = new LinkedList<>();
    }
    
    public void enqueue(T element) {
        queue.add(element);
    }
    
    public T dequeue() {
        if (isEmpty()) {
            throw new NoSuchElementException();
        }
        return queue.remove(0);
    }
    
    public T peek() {
        if (isEmpty()) {
            throw new NoSuchElementException();
        }
        return queue.get(0);
    }
    
    public boolean isEmpty() {
        return queue.isEmpty();
    }
    
    public int size() {
        return queue.size();
    }
}
```

In the above code, we have implemented a generic custom queue class using a Java wrapper class LinkedList. The `enqueue` method adds an element to the end of the queue, while the `dequeue` method removes and returns the first element. The `peek` method returns the first element without removing it. The `isEmpty` method checks if the queue is empty, and the `size` method returns the current size of the queue.

## Conclusion

Using wrapper classes in Java, we can easily implement custom data structures like stacks and queues. These wrapper classes provide the necessary methods and behaviors to work with our custom data structures efficiently. By encapsulating our data within these wrapper classes, we can easily extend and modify the functionality as per our requirements.

So, next time you need to implement a custom data structure in Java, consider using wrapper classes to simplify the process and improve the readability of your code.

#customdatastructures #javawrappers