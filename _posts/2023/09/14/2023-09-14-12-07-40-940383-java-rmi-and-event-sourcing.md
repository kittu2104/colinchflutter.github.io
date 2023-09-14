---
layout: post
title: "Java RMI and event sourcing"
description: " "
date: 2023-09-14
tags: [JavaRMI, EventSourcing]
comments: true
share: true
---

Java Remote Method Invocation (RMI) is a powerful technology that enables developers to build distributed applications in Java. It allows you to invoke methods on remote objects, making it possible to create applications that span multiple machines and communicate seamlessly over a network.

## How Does Java RMI Work?

At its core, Java RMI relies on a client-server model. The server exposes a set of objects that can be accessed remotely by clients. When the client calls a method on a remote object, RMI takes care of marshaling and unmarshaling the method arguments and return values, as well as providing the communication infrastructure to transmit these messages between the client and server.

Here's a simplified example that demonstrates Java RMI:

```java
// Server code
public interface HelloWorld extends Remote {
  String sayHello() throws RemoteException;
}

public class HelloWorldImpl extends UnicastRemoteObject implements HelloWorld {
  public HelloWorldImpl() throws RemoteException {}

  public String sayHello() throws RemoteException {
    return "Hello, world!";
  }

  public static void main(String[] args) {
    try {
      HelloWorld helloWorld = new HelloWorldImpl();
      Naming.rebind("HelloWorld", helloWorld);
      System.out.println("Server started!");
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}

// Client code
public class HelloWorldClient {
  public static void main(String[] args) {
    try {
      HelloWorld helloWorld = (HelloWorld) Naming.lookup("rmi://localhost/HelloWorld");
      String message = helloWorld.sayHello();
      System.out.println("Server says: " + message);
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```

In this example, the server exposes the `HelloWorld` interface and its implementation `HelloWorldImpl` using RMI. The client uses RMI to locate and invoke the remote `sayHello` method on the server.

Make sure to run the RMI registry before executing the server and client code:
```bash
rmiregistry
```

# Event Sourcing: Storing State Changes

Event sourcing is a pattern often used in distributed systems to capture and store the state changes of an application over time. Instead of directly updating the state of an object or entity, event sourcing preserves a history of events that have occurred, which can be replayed to obtain the current state.

## How Does Event Sourcing Work?

The idea behind event sourcing is simple: instead of storing the current state of an object or entity, we store a log of events that have happened in the past. Each event represents a change in the state and is immutable. By applying events in chronological order, we can reconstruct the state of an object or entity at any given point in time.

Event sourcing provides several benefits, including:

- **Auditability**: The event log retains a complete history of all changes, providing a detailed audit trail.
- **Reproducibility**: By replaying events from the log, you can reproduce past states or debug issues.
- **Scalability**: Event sourcing allows for easy scaling as the system can process events asynchronously and distribute processing across multiple nodes.

One popular implementation of event sourcing in Java is the Axon Framework. It provides a powerful set of tools for building event-driven applications using the event sourcing pattern.

```java
// Command
public class CreatePaymentCommand {
  private String paymentId;
  private BigDecimal amount;
  // ... other fields

  // getters, setters, constructor
}

// Event
public class PaymentCreatedEvent {
  private String paymentId;
  private BigDecimal amount;
  // ... other fields

  // getters, setters, constructor
}

// Aggregate
public class PaymentAggregate {
  @AggregateIdentifier
  private String paymentId;
  private BigDecimal amount;
  // ... other fields

  @CommandHandler
  public PaymentAggregate(CreatePaymentCommand command) {
    // Apply event and update state
    apply(new PaymentCreatedEvent(command.getPaymentId(), command.getAmount()));
  }
  
  @EventSourcingHandler
  public void on(PaymentCreatedEvent event) {
    // Update state using event
    this.paymentId = event.getPaymentId();
    this.amount = event.getAmount();
    // ...
  }
  // ... other methods
}
```

In this example, `CreatePaymentCommand` represents a command to create a payment. When this command is received, the `PaymentAggregate` is instantiated and applies the `PaymentCreatedEvent`, which captures the state change. The `@EventSourcingHandler` method updates the state based on the event.

Event sourcing allows for easy scalability and the ability to replay events to derive the current state of an object or entity, making it a valuable pattern for building distributed systems.

# Hashtags: #JavaRMI #EventSourcing