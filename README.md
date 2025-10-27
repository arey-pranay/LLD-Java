# 📘 Low-Level System Design Basics – OOP & SOLID Principles

Understanding **Object-Oriented Programming (OOP)** and the **SOLID principles** is a non-negotiable step for excelling in **Low-Level System Design (LLD)**. These principles help build scalable, maintainable, and reusable systems — crucial for LLD interviews and real-world system architecture.
{Course Repository}[https://github.com/prateek27/design-patterns-java/tree/main]{Course Repository}
---

## 🔷 Object-Oriented Programming (OOP)

Object-Oriented Programming is a programming paradigm based on the concept of **"objects"**, which can contain data and code: data in the form of fields (attributes), and code in the form of procedures (methods).

### 1. Encapsulation
**Definition**: Encapsulation is the practice of wrapping data (variables) and methods that operate on the data into a single unit or class and restricting access to some of the object’s components.

**Usage**: Protect internal object states and enforce access control.

**Java Example**:
```java
public class BankAccount {
    private double balance;

    public BankAccount(double balance) {
        this.balance = balance;
    }

    public void deposit(double amount) {
        if(amount > 0) {
            balance += amount;
        }
    }

    public double getBalance() {
        return balance;
    }
}
````

---

### 2. Abstraction

**Definition**: Abstraction is hiding complex implementation details and exposing only the essential features of an object.

**Usage**: Simplifies interaction with complex systems and reduces coupling.

**Java Example**:

```java
abstract class Vehicle {
    abstract void start();
    abstract void stop();
}

class Car extends Vehicle {
    @Override
    void start() {
        System.out.println("Car started");
    }

    @Override
    void stop() {
        System.out.println("Car stopped");
    }
}
```

---

### 3. Inheritance

**Definition**: Inheritance is the mechanism by which one class acquires the properties and behaviors of another class.

**Usage**: Promotes code reuse and polymorphic behavior.

**Java Example**:

```java
class Animal {
    void sound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Bark");
    }
}
```

---

### 4. Polymorphism

**Definition**: Polymorphism means the ability to take many forms. It allows methods to do different things based on the object it is acting upon.

**Types**:

* **Compile-Time (Method Overloading)**
* **Run-Time (Method Overriding)**

**Java Example – Overloading**:

```java
class MathUtil {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

**Java Example – Overriding**:

```java
class Animal {
    void sound() {
        System.out.println("Some sound");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Meow");
    }
}
```

---

## 🔷 SOLID Principles

SOLID is an acronym for five design principles intended to make software designs more understandable, flexible, and maintainable.

---

### ✅ 1. Single Responsibility Principle (SRP)

**Definition**: A class should have only one reason to change.

**Usage**: Separates concerns and reduces complexity.

**Java Example**:

```java
class Report {
    String reportContent;

    public String getContent() {
        return reportContent;
    }
}

class ReportPrinter {
    void printReport(Report report) {
        System.out.println(report.getContent());
    }
}
```

---

### ✅ 2. Open/Closed Principle (OCP)

**Definition**: Software entities should be open for extension but closed for modification.

**Usage**: Extending system behavior without modifying existing code.

**Java Example**:

```java
interface Notification {
    void send(String message);
}

class EmailNotification implements Notification {
    public void send(String message) {
        System.out.println("Email: " + message);
    }
}

class SMSNotification implements Notification {
    public void send(String message) {
        System.out.println("SMS: " + message);
    }
}
```

---

### ✅ 3. Liskov Substitution Principle (LSP)

**Definition**: Subtypes must be substitutable for their base types.

**Usage**: Ensure derived classes extend base class functionality without altering expected behavior.

**Java Example**:

```java
class Bird {
    public void fly() {
        System.out.println("Flying");
    }
}

class Sparrow extends Bird {}

class Ostrich extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Ostriches can't fly");
    }
}
```

🔧 **Fix**:

```java
interface Flyable {
    void fly();
}

class Sparrow implements Flyable {
    public void fly() {
        System.out.println("Sparrow flying");
    }
}
```

---

### ✅ 4. Interface Segregation Principle (ISP)

**Definition**: No client should be forced to depend on interfaces it does not use.

**Usage**: Split large interfaces into smaller ones.

**Java Example**:

```java
interface Workable {
    void work();
}

interface Feedable {
    void eat();
}

class HumanWorker implements Workable, Feedable {
    public void work() {
        System.out.println("Human working");
    }

    public void eat() {
        System.out.println("Human eating");
    }
}

class RobotWorker implements Workable {
    public void work() {
        System.out.println("Robot working");
    }
}
```

---

### ✅ 5. Dependency Inversion Principle (DIP)

**Definition**: Depend on abstractions, not on concrete classes.

**Usage**: Reduces coupling between high- and low-level modules.

**Java Example**:

```java
interface Keyboard {
    void type();
}

class MechanicalKeyboard implements Keyboard {
    public void type() {
        System.out.println("Typing with mechanical keyboard");
    }
}

class Computer {
    private Keyboard keyboard;

    public Computer(Keyboard keyboard) {
        this.keyboard = keyboard;
    }

    public void input() {
        keyboard.type();
    }
}
```

---

## 🛠 Why This Matters for Low-Level Design (LLD)

These principles help in:

* Structuring classes and interfaces clearly
* Enabling reusability and flexibility
* Avoiding tight coupling and improving scalability
* Building robust foundations for LLD interview problems like:

  * Parking Lot
  * BookMyShow
  * Elevator System
  * Splitwise, etc.

---

## 🔗 Links

* 🎓 [Udemy Course – Low Level System Design, Design Patterns & SOLID Principles](https://www.udemy.com/share/10c6GX3@RIK5zdqMcdlA-DBmr2VVpeTTrWWuzmFMWWJ_JmNFjv-KObcoxxJ7rURDTH6o69ahMQ==/)
* 📝 [My detailed OOPS Notes](https://github.com/arey-pranay/OOPS_InterviewPrep/blob/main/README.md)
---

**Happy Designing! 🧠**

```
