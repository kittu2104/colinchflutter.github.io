---
layout: post
title: "Implementing distributed task scheduling using Java RMI"
description: " "
date: 2023-09-14
tags: []
comments: true
share: true
---

In distributed systems, task scheduling plays a crucial role in efficiently utilizing resources across multiple machines. Java RMI (Remote Method Invocation) provides a way to execute remote methods on different Java Virtual Machines (JVMs) over a network. In this blog post, we will discuss how to implement a distributed task scheduling system using Java RMI.

## Prerequisites
- Basic knowledge of Java programming language
- Familiarity with Java RMI concepts

## Step 1: Define the Task Interface
To start, we need to define the interface that represents the tasks to be executed. This interface will include the methods that the tasks should implement.

```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface Task extends Remote {
    public void execute() throws RemoteException;
}
```

Here, we define a `Task` interface that extends the `Remote` interface from the `java.rmi` package. The `execute` method represents the task to be executed and is declared to throw a `RemoteException`.

## Step 2: Implement the Task
Next, we need to implement the `Task` interface with the actual logic of the task that needs to be executed. Let's create a `PrintTask` class as an example.

```java
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;

public class PrintTask extends UnicastRemoteObject implements Task {
    private String message;

    public PrintTask(String message) throws RemoteException {
        this.message = message;
    }

    public void execute() throws RemoteException {
        System.out.println(message);
    }
}
```

The `PrintTask` class extends `UnicastRemoteObject` to provide the necessary infrastructure for remote method invocation. We implement the `execute` method to print the stored message.

## Step 3: Create the Server
Now, we need to create a server that acts as a task scheduler and executes the remote tasks. Let's create a `TaskSchedulerServer` class.

```java
import java.rmi.Naming;
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;
import java.util.ArrayList;
import java.util.List;

public class TaskSchedulerServer {
    private static List<Task> taskList;

    public static void main(String[] args) {
        try {
            taskList = new ArrayList<Task>();

            TaskScheduler taskScheduler = new TaskSchedulerImpl(taskList);
            TaskScheduler stub = (TaskScheduler) UnicastRemoteObject.exportObject(taskScheduler, 0);

            Naming.rebind("//localhost/TaskScheduler", stub);

            System.out.println("TaskSchedulerServer ready!");
        } catch (Exception e) {
            System.err.println("TaskSchedulerServer exception: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

The `TaskSchedulerServer` class binds the `TaskScheduler` implementation to the RMI registry using `Naming.rebind` method. It also initializes a list to store the tasks received from the clients.

## Step 4: Create the Task Scheduler
The task scheduler will receive tasks from the clients and execute them. Let's create a `TaskScheduler` interface and its implementation.

```java
import java.rmi.Remote;
import java.rmi.RemoteException;
import java.util.List;

public interface TaskScheduler extends Remote {
    public void scheduleTask(Task task) throws RemoteException;
    public List<Task> getTaskList() throws RemoteException;
}
```

```java
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;
import java.util.List;

public class TaskSchedulerImpl extends UnicastRemoteObject implements TaskScheduler {
    private List<Task> taskList;

    public TaskSchedulerImpl(List<Task> taskList) throws RemoteException {
        this.taskList = taskList;
    }

    public void scheduleTask(Task task) throws RemoteException {
        taskList.add(task);
        task.execute();
    }

    public List<Task> getTaskList() throws RemoteException {
        return taskList;
    }
}
```

Here, the `TaskSchedulerImpl` class implements the `TaskScheduler` interface and provides the implementation for scheduling the tasks and retrieving the task list.

## Step 5: Create the Client
Finally, let's create a client application that can submit tasks to the task scheduler. 

```java
import java.rmi.Naming;
import java.util.Scanner;

public class TaskSchedulerClient {
    public static void main(String[] args) {
        try {
            TaskScheduler taskScheduler = (TaskScheduler) Naming.lookup("//localhost/TaskScheduler");

            Scanner scanner = new Scanner(System.in);
            System.out.println("Enter a message to schedule a task (or 'exit' to quit):");
            String message = scanner.nextLine();

            while (!message.equals("exit")) {
                Task task = new PrintTask(message);
                taskScheduler.scheduleTask(task);

                System.out.println("Task scheduled.");

                System.out.println("Enter a message to schedule a task (or 'exit' to quit):");
                message = scanner.nextLine();
            }
        } catch (Exception e) {
            System.err.println("TaskSchedulerClient exception: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

The `TaskSchedulerClient` class looks up the remote `TaskScheduler` object using `Naming.lookup` and prompts the user to enter a message. It creates a `PrintTask` instance with the entered message and submits it to the task scheduler.

## Conclusion
By utilizing Java RMI, we were able to implement a distributed task scheduling system where tasks can be submitted from a client and executed on a server. This enables efficient utilization of resources across multiple machines in a distributed system.