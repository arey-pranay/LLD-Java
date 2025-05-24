# 🎯 Behavioral Design Patterns in Java

**Behavioral Design Patterns** define **how objects interact** and **delegate responsibilities**. These patterns are crucial for building maintainable and scalable software systems, especially when behaviors change dynamically or multiple objects collaborate.

---

## 📚 Overview

**Definition:** Behavioral patterns are design patterns that identify common communication patterns between objects and realize these patterns to increase flexibility in carrying out communication.

**Purpose:**  
- Manage algorithms, relationships, and responsibilities
- Decouple classes to improve maintainability
- Enhance object collaboration
---

## 🔁 1. Observer Pattern

**Definition**: Defines a one-to-many dependency between objects. When one object (subject) changes state, all its dependents (observers) are notified automatically.

**Use Case**: Event listeners, notification systems.

**Java Example**:
```java
interface Observer {
    void update(String message);
}

class User implements Observer {
    private String name;

    User(String name) { this.name = name; }

    public void update(String message) {
        System.out.println(name + " received: " + message);
    }
}

class NotificationService {
    private List<Observer> observers = new ArrayList<>();

    void addObserver(Observer o) { observers.add(o); }
    void removeObserver(Observer o) { observers.remove(o); }

    void notifyObservers(String message) {
        for (Observer o : observers) {
            o.update(message);
        }
    }
}
````

**📌 Intent**: Define a one-to-many relationship. When the subject changes, all observers are notified.

**🧠 When to Use**:
- Multiple objects need to react to state changes in another object.
- You want to implement event-driven systems.

**✅ Benefits**:
- Loose coupling between subject and observers
- Easy to add/remove observers dynamically

---

## ⚙️ 2. Strategy Pattern


**Definition**: Allows a family of algorithms to be defined and made interchangeable. The algorithm can vary independently from the clients using it.

**Use Case**: Payment methods, compression algorithms, sorting.

**Java Example**:

```java
interface PaymentStrategy {
    void pay(int amount);
}

class CreditCardPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid $" + amount + " using Credit Card");
    }
}

class PayPalPayment implements PaymentStrategy {
    public void pay(int amount) {
        System.out.println("Paid $" + amount + " using PayPal");
    }
}

class ShoppingCart {
    private PaymentStrategy strategy;

    ShoppingCart(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    void checkout(int amount) {
        strategy.pay(amount);
    }
}
```

**📌 Intent**: Define a family of algorithms and make them interchangeable without changing the context.

**🧠 When to Use**:
- You need different ways to perform a task (e.g., multiple sorting or payment strategies).
- You want to avoid conditional logic (if-else chains).

**✅ Benefits**:
- Promotes Open/Closed Principle
- Simplifies unit testing by injecting different strategies

---

## 🕹 3. Command Pattern
 

**Definition**: Encapsulates a request as an object, thereby allowing users to parameterize clients with queues, requests, and operations.

**Use Case**: Undo functionality, job queues, remote control apps.

**Java Example**:

```java
interface Command {
    void execute();
}

class Light {
    void on() { System.out.println("Light ON"); }
    void off() { System.out.println("Light OFF"); }
}

class LightOnCommand implements Command {
    private Light light;

    LightOnCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.on();
    }
}

class RemoteControl {
    private Command command;

    void setCommand(Command command) {
        this.command = command;
    }

    void pressButton() {
        command.execute();
    }
}
```
**📌 Intent**: Encapsulate a request as an object, allowing parameterization, queuing, and logging.

**🧠 When to Use**:
- You need undo/redo features.
- You want to decouple sender from receiver of a request.
- You’re implementing job queues or transactional systems.

**✅ Benefits**:
- Decouples request handling
- Can log, queue, and undo commands

---

## 🧬 4. Template Method Pattern

**📌 Intent**: Define a fixed algorithm structure and allow subclasses to override certain steps.

**🧠 When to Use**:
- You want to reuse code but allow customizable steps.
- You’re implementing workflows or pipelines.

**✅ Benefits**:
- Promotes code reuse
- Allows variations in behavior without modifying structure

---

## 🔄 5. Iterator Pattern

**📌 Intent**: Provide a standard way to access elements of a collection sequentially.

**🧠 When to Use**:
- You want to access collection items without exposing internals.
- You want to implement custom traversals.

**✅ Benefits**:
- Unified way of accessing elements
- Supports multiple traversal algorithms

---

## 🌀 6. State Pattern

**📌 Intent**: Allow an object to change its behavior when its internal state changes.

**🧠 When to Use**:
- Object behavior depends on its state.
- You want to avoid massive conditionals (if-else or switch).

**✅ Benefits**:
- Cleaner and modular state transitions
- Easier to add new states

---

## 🧭 7. Mediator Pattern

**📌 Intent**: Encapsulate object interactions in a mediator so objects don’t communicate directly.

**🧠 When to Use**:
- Complex communication logic exists between multiple objects.
- You want to reduce coupling and centralize behavior.

**✅ Benefits**:
- Simplifies communication
- Makes object behavior more reusable

---

## 🧠 8. Memento Pattern

**📌 Intent**: Capture and restore an object's internal state without violating encapsulation.

**🧠 When to Use**:
- Implementing undo/redo
- You need checkpoints or history (e.g., game save states)

**✅ Benefits**:
- Preserves encapsulation
- Enables state restoration easily

---

## 📊 Summary Table

| Pattern           | Use Case Example           | Intent                                       | Key Benefit                        |
|------------------|----------------------------|----------------------------------------------|------------------------------------|
| **Observer**      | Notification systems       | Publish/subscribe to changes                 | Decouples data source from views   |
| **Strategy**      | Payment methods            | Switchable algorithms at runtime             | Interchangeable behavior           |
| **Command**       | Undo in editors            | Encapsulate actions                          | Flexible command management        |
| **Template Method** | Game loop, parsing       | Algorithm structure with extensible steps    | Code reuse + flexibility           |
| **Iterator**      | List traversal             | Standard way to access collections           | Uniform traversal                  |
| **State**         | Vending machine            | Change behavior based on internal state      | Eliminates large conditional logic |
| **Mediator**      | Chat app, UI form fields   | Centralized communication between components | Loose coupling                     |
| **Memento**       | Versioning, undo/redo      | Save and restore object state                | Preserves internal state privately |

---
