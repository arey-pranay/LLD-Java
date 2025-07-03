# 🏗️ Creational Design Patterns in Java

**Creational Design Patterns** abstract the instantiation process. They help make the system independent of how its objects are created, composed, and represented.

---

## 📚 Overview

**Definition:** Creational patterns deal with object creation mechanisms, trying to create objects in a manner suitable to the situation.

**Purpose:**

* Encapsulate object creation logic
* Improve flexibility and reuse
* Decouple object instantiation from usage

---

## 🔁 1. Singleton Pattern

**Definition**: Ensures a class has only one instance and provides a global point of access to it.

**Use Case**: Logging, configuration, cache, DB connection.

**Java Example**:

```java
class Singleton {
    private static Singleton instance;

    private Singleton() {}

    public static Singleton getInstance() {
        if (instance == null)
            instance = new Singleton();
        return instance;
    }

    public void log(String message) {
        System.out.println("Log: " + message);
    }
}
```

**📌 Intent**: Guarantee a single instance and provide a global point of access.

**🧠 When to Use**:

* Single point of control is needed
* Resource-heavy objects like DB connection, configuration

**✅ Benefits**:

* Controlled access
* Saves resources by preventing unnecessary instantiation

---

## 🏭 2. Factory Method Pattern

**Definition**: Defines an interface for creating an object, but lets subclasses alter the type of objects that will be created.

**Use Case**: Shape creation, UI components, parsing logic.

**Java Example**:

```java
interface Shape {
    void draw();
}

class Circle implements Shape {
    public void draw() {
        System.out.println("Drawing Circle");
    }
}

class Square implements Shape {
    public void draw() {
        System.out.println("Drawing Square");
    }
}

class ShapeFactory {
    public static Shape getShape(String type) {
        if (type.equals("circle")) return new Circle();
        else if (type.equals("square")) return new Square();
        return null;
    }
}
```

**📌 Intent**: Delegate object creation to a method or subclass.

**🧠 When to Use**:

* You need to abstract object creation logic
* You want to create objects without binding to specific classes

**✅ Benefits**:

* Decouples object creation from usage
* Adds flexibility for future extensions

---

## 🧰 3. Abstract Factory Pattern

**Definition**: Produces families of related or dependent objects without specifying their concrete classes.

**Use Case**: UI themes, cross-platform components.

**Java Example**:

```java
interface Button {
    void render();
}

class WindowsButton implements Button {
    public void render() { System.out.println("Windows Button"); }
}

class MacButton implements Button {
    public void render() { System.out.println("Mac Button"); }
}

interface GUIFactory {
    Button createButton();
}

class WindowsFactory implements GUIFactory {
    public Button createButton() {
        return new WindowsButton();
    }
}

class MacFactory implements GUIFactory {
    public Button createButton() {
        return new MacButton();
    }
}
```

**📌 Intent**: Provide an interface for creating families of related objects without specifying their classes.

**🧠 When to Use**:

* You need to create related objects across different variants/platforms
* You want to enforce consistency between components

**✅ Benefits**:

* Enforces design consistency
* Easy to switch families (themes, OS, etc.)

---

## 🧱 4. Builder Pattern

**Definition**: Separates the construction of a complex object from its representation so the same construction process can create different representations.

**Use Case**: Object with many optional fields (e.g., user profile, form data).

**Java Example**:

```java
class User {
    private String name;
    private int age;
    private String address;

    public static class Builder {
        private String name;
        private int age;
        private String address;

        public Builder setName(String name) {
            this.name = name; return this;
        }

        public Builder setAge(int age) {
            this.age = age; return this;
        }

        public Builder setAddress(String address) {
            this.address = address; return this;
        }

        public User build() {
            User user = new User();
            user.name = this.name;
            user.age = this.age;
            user.address = this.address;
            return user;
        }
    }

    public void show() {
        System.out.println(name + ", " + age + ", " + address);
    }
}
```

**📌 Intent**: Simplify the creation of complex objects with many configuration options.

**🧠 When to Use**:

* Objects have many optional attributes
* You want immutable objects with clean code

**✅ Benefits**:

* Cleaner object construction
* Supports immutability and readability

---

## 🧬 5. Prototype Pattern

**Definition**: Creates new objects by cloning existing ones instead of instantiating from scratch.

**Use Case**: Object duplication with similar structure (e.g., game units, templates).

**Java Example**:

```java
class Document implements Cloneable {
    private String content;

    public Document(String content) {
        this.content = content;
    }

    public void setContent(String content) {
        this.content = content;
    }

    public Document clone() throws CloneNotSupportedException {
        return (Document) super.clone();
    }

    public void print() {
        System.out.println("Document: " + content);
    }
}
```

**📌 Intent**: Copy objects without depending on their concrete classes.

**🧠 When to Use**:

* Creating objects is expensive
* You want to avoid re-initializing a similar object

**✅ Benefits**:

* Reduces cost of creating similar objects
* Faster and simpler instantiation

---

## 📊 Summary Table

| Pattern              | Use Case Example         | Intent                            | Key Benefit                       |
| -------------------- | ------------------------ | --------------------------------- | --------------------------------- |
| **Singleton**        | Logger, DB connection    | One instance globally accessible  | Controlled instantiation          |
| **Factory Method**   | Shape factory            | Abstract object creation          | Decouples logic from class        |
| **Abstract Factory** | GUI themes (Windows/Mac) | Families of related objects       | Consistent product families       |
| **Builder**          | User form                | Build complex object step-by-step | Better readability, flexibility   |
| **Prototype**        | Game units, templates    | Clone existing object             | Fast and memory-efficient cloning |

