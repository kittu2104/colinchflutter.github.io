---
layout: post
title: "Creating a simple Java RMI application"
description: " "
date: 2023-09-14
tags: [JavaRMI, DistributedSystems]
comments: true
share: true
---

In this tutorial, we will walk through the process of creating a simple Java RMI (Remote Method Invocation) application. RMI is a Java API that allows objects running on one JVM (Java Virtual Machine) to invoke methods on objects running in another JVM.

## Prerequisites
* Java Development Kit (JDK) installed
* Basic understanding of Java programming

## Step 1: Define the Remote Interface
* Create a new Java interface `MyRemoteInterface.java`.
* Declare the methods that will be remotely accessed by clients.
* Add the `RemoteException` declaration to the method signatures.
```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface MyRemoteInterface extends Remote {
    // Remote method declarations
    String sayHello(String name) throws RemoteException;
}
```

## Step 2: Implement the Remote Interface
* Create a new Java class `MyRemoteImpl.java` that implements the remote interface.
* Implement the methods declared in the interface.
```java
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;

public class MyRemoteImpl extends UnicastRemoteObject implements MyRemoteInterface {
    public MyRemoteImpl() throws RemoteException {
        // Required to satisfy the constructor of UnicastRemoteObject
    }

    @Override
    public String sayHello(String name) throws RemoteException {
        return "Hello, " + name + "!";
    }
}
```

## Step 3: Create the Server
* Create a new Java class `RMIServer.java` that will act as the server.
* In the `main` method, start the RMI registry and bind the remote object to a name.
```java
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class RMIServer {
    public static void main(String[] args) {
        try {
            // Start the RMI registry
            Registry registry = LocateRegistry.createRegistry(1099);
    
            // Create an instance of the remote object
            MyRemoteInterface remoteObject = new MyRemoteImpl();
    
            // Bind the remote object to a name in the registry
            registry.bind("MyRemoteObject", remoteObject);
    
            System.out.println("Server started");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Step 4: Create the Client
* Create a new Java class `RMIClient.java` that will act as the client.
* In the `main` method, lookup the remote object and invoke remote methods.
```java
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class RMIClient {
    public static void main(String[] args) {
        try {
            // Get a reference to the RMI registry
            Registry registry = LocateRegistry.getRegistry("localhost");
    
            // Lookup the remote object by name
            MyRemoteInterface remoteObject = (MyRemoteInterface) registry.lookup("MyRemoteObject");
    
            // Invoke remote methods
            String response = remoteObject.sayHello("John");
            System.out.println(response);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## Step 5: Run the Application
* Compile all the Java files using the JDK compiler.
```bash
javac MyRemoteInterface.java MyRemoteImpl.java RMIServer.java RMIClient.java
```

* Start the server by running the `RMIServer` class.
```bash
java RMIServer
```

* Start the client by running the `RMIClient` class.
```bash
java RMIClient
```

## Conclusion
Congratulations! You have successfully created a simple Java RMI application. RMI provides a powerful mechanism for developing distributed Java applications by allowing objects to invoke methods on remote objects. This basic example can serve as a foundation for more complex distributed systems. #JavaRMI #DistributedSystems