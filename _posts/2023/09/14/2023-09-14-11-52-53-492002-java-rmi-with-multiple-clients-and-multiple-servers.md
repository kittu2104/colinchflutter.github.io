---
layout: post
title: "Java RMI with multiple clients and multiple servers"
description: " "
date: 2023-09-14
tags: [JavaRMI, DistributedSystems]
comments: true
share: true
---

In this blog post, we will explore how to implement Java RMI (Remote Method Invocation) with multiple clients and multiple servers. RMI is a powerful technology in Java that allows objects in different Java Virtual Machines (JVMs) to communicate with each other.

## Setting Up the Environment

To begin, make sure you have the following installed on your machine:
- Java Development Kit (JDK)
- Integrated Development Environment (IDE) of your choice (such as Eclipse, IntelliJ, or NetBeans)

## Creating the Server

Let's start by creating a server class that will provide the remote service to clients. Here's an example:

```java
import java.rmi.*;
import java.rmi.server.*;

public class Server extends UnicastRemoteObject implements RemoteService {

    protected Server() throws RemoteException {
        super();
    }

    public static void main(String[] args) {
        try {
            // Create remote service object
            RemoteService service = new Server();

            // Bind the service to a specific port
            Naming.rebind("rmi://localhost:1099/Service", service);

            System.out.println("Server running...");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    @Override
    public String sayHello(String name) throws RemoteException {
        return "Hello, " + name + "!";
    }
}
```

In this example, we create a class `Server` that implements the `RemoteService` interface. The `RemoteService` interface defines the methods that can be invoked remotely by the clients. In this case, we have a single method `sayHello` that takes a name and returns a greeting.

In the `main` method, we create an instance of the server object and bind it to the RMI registry at `rmi://localhost:1099/Service`.

## Creating the Client

Now let's create a client class that will access the remote service provided by the server. Here's an example:

```java
import java.rmi.*;

public class Client {

    public static void main(String[] args) {
        try {
            // Get the remote service object from the RMI registry
            RemoteService service = (RemoteService) Naming.lookup("rmi://localhost:1099/Service");

            // Invoke the remote method
            String response = service.sayHello("John Doe");

            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

In this example, we retrieve the remote service object using the `Naming.lookup` method and the RMI registry URL `rmi://localhost:1099/Service`. We then invoke the `sayHello` method on the remote service and print the response.

## Running Multiple Clients and Servers

To run multiple clients and servers, you need to ensure that each server and client is running on a different port. You can change the port number in the server URL, for example, `rmi://localhost:1100/Service`.

Start multiple server instances on different ports and then run the client code to interact with each server.

## Conclusion

Java RMI provides a simple and powerful way to implement distributed systems with remote method invocation. By creating multiple clients and servers, you can build scalable and distributed applications. Explore further by implementing more methods and adding additional features to meet your specific requirements.

#JavaRMI #DistributedSystems