

### 1. **Bridge Pattern**

#### **Intent:**

The **Bridge Pattern** is a structural design pattern that separates an abstraction from its implementation so that both can evolve independently. The key idea is to decouple the abstraction (interface) from its concrete implementation.

#### **Structure:**

* **Abstraction**: Defines the abstract interface that clients use.
* **RefinedAbstraction**: Extends the Abstraction class and refines it further.
* **Implementor**: Defines the interface for implementation classes.
* **ConcreteImplementor**: Provides the concrete implementation of the Implementor interface.

#### **Use Case:**

The **Bridge Pattern** is useful when:

* You need to decouple an abstraction from its implementation.
* Both abstraction and implementation need to be extended independently.
* You want to avoid creating a large number of subclasses for different combinations of abstractions and implementations.

#### **Example:**

```java
// Implementor
interface Color {
    void fill();
}

// ConcreteImplementor
class Red implements Color {
    @Override
    public void fill() {
        System.out.println("Filling with Red color");
    }
}

class Blue implements Color {
    @Override
    public void fill() {
        System.out.println("Filling with Blue color");
    }
}

// Abstraction
abstract class Shape {
    protected Color color;

    public Shape(Color color) {
        this.color = color;
    }

    abstract void draw();
}

// RefinedAbstraction
class Circle extends Shape {
    public Circle(Color color) {
        super(color);
    }

    @Override
    void draw() {
        System.out.print("Drawing Circle with ");
        color.fill();
    }
}

class Square extends Shape {
    public Square(Color color) {
        super(color);
    }

    @Override
    void draw() {
        System.out.print("Drawing Square with ");
        color.fill();
    }
}

// Client code
public class BridgePatternDemo {
    public static void main(String[] args) {
        Shape redCircle = new Circle(new Red());
        Shape blueSquare = new Square(new Blue());

        redCircle.draw();
        blueSquare.draw();
    }
}
```

#### **Key Points:**

* The **Shape** class (Abstraction) is decoupled from the **Color** class (Implementor).
* You can easily switch between shapes and colors, and extend them independently without affecting other components.

---

### 2. **Visitor Pattern**

#### **Intent:**

The **Visitor Pattern** is a behavioral design pattern that allows you to add further operations to objects without modifying them. It lets you define new operations on a set of objects without changing the classes of the elements on which it operates.

#### **Structure:**

* **Visitor**: Interface that declares a visit method for each element type.
* **ConcreteVisitor**: Implements the visit methods defined in the Visitor interface.
* **Element**: Interface that accepts the visitor.
* **ConcreteElement**: Implements the Element interface, representing the structure to which operations can be added.
* **ObjectStructure**: A collection of Elements that can accept visitors.

#### **Use Case:**

* When you need to perform operations across a set of objects in a structure.
* When you need to add new operations to objects without changing their classes.

#### **Example:**

```java
// Visitor Interface
interface Visitor {
    void visit(Book book);
    void visit(Magazine magazine);
}

// ConcreteVisitor
class PriceVisitor implements Visitor {
    @Override
    public void visit(Book book) {
        System.out.println("Book Price: " + book.getPrice());
    }

    @Override
    public void visit(Magazine magazine) {
        System.out.println("Magazine Price: " + magazine.getPrice());
    }
}

// Element Interface
interface Element {
    void accept(Visitor visitor);
}

// ConcreteElement
class Book implements Element {
    private double price;

    public Book(double price) {
        this.price = price;
    }

    public double getPrice() {
        return price;
    }

    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

class Magazine implements Element {
    private double price;

    public Magazine(double price) {
        this.price = price;
    }

    public double getPrice() {
        return price;
    }

    @Override
    public void accept(Visitor visitor) {
        visitor.visit(this);
    }
}

// Client code
public class VisitorPatternDemo {
    public static void main(String[] args) {
        Element[] elements = new Element[] {
            new Book(12.99),
            new Magazine(5.99)
        };

        Visitor priceVisitor = new PriceVisitor();

        for (Element element : elements) {
            element.accept(priceVisitor);
        }
    }
}
```

#### **Key Points:**

* The **Visitor** pattern allows new operations (like `PriceVisitor`) to be added to existing objects (like `Book` and `Magazine`) without modifying their structure.
* The **accept** method in each element class (like `Book` and `Magazine`) allows the visitor to perform operations on the object.

<img width="1671" height="994" alt="image" src="https://github.com/user-attachments/assets/000fa372-ef2f-4eb8-bea4-f2d39dd11c72" />


---

### 3. **Chain of Responsibility Pattern**

#### **Intent:**

The **Chain of Responsibility Pattern** is a behavioral design pattern that allows a request to be passed along a chain of handlers. Each handler in the chain either processes the request or passes it on to the next handler in the chain. This pattern decouples the sender and receiver of a request, allowing multiple handlers to process the request independently.

#### **Structure:**

* **Handler**: Defines an abstract handler for processing the request and a reference to the next handler in the chain.
* **ConcreteHandler**: Handles the request or passes it to the next handler.
* **Client**: Initiates the request.

#### **Use Case:**

* When you want to pass a request along a chain of handlers.
* When a single request can be handled by multiple classes in a sequence.
* When the exact handler that processes the request should be determined at runtime.

#### **Example:**

```java
// Handler Interface
abstract class Handler {
    protected Handler nextHandler;

    public void setNextHandler(Handler nextHandler) {
        this.nextHandler = nextHandler;
    }

    public abstract void handleRequest(String request);
}

// ConcreteHandler1
class ConcreteHandler1 extends Handler {
    @Override
    public void handleRequest(String request) {
        if (request.equals("Request1")) {
            System.out.println("Handler1 handled the request.");
        } else if (nextHandler != null) {
            nextHandler.handleRequest(request);
        }
    }
}

// ConcreteHandler2
class ConcreteHandler2 extends Handler {
    @Override
    public void handleRequest(String request) {
        if (request.equals("Request2")) {
            System.out.println("Handler2 handled the request.");
        } else if (nextHandler != null) {
            nextHandler.handleRequest(request);
        }
    }
}

// Client code
public class ChainOfResponsibilityPatternDemo {
    public static void main(String[] args) {
        Handler handler1 = new ConcreteHandler1();
        Handler handler2 = new ConcreteHandler2();

        handler1.setNextHandler(handler2);

        // Chain of responsibility
        handler1.handleRequest("Request1");
        handler1.handleRequest("Request2");
        handler1.handleRequest("Request3"); // Will be passed to next handler
    }
}
```

#### **Key Points:**

* The request is passed through the chain of handlers.
* Each handler decides whether to process the request or pass it on to the next handler.
* The **Chain of Responsibility** allows dynamic assignment of handlers, making it easy to add new handlers without affecting the rest of the system.

---

### Conclusion:

* **Bridge Pattern** is useful when you want to decouple abstractions from their implementations.
* **Visitor Pattern** allows you to add new operations to existing classes without changing them.
* **Chain of Responsibility Pattern** gives you a flexible and decoupled approach to handling requests through a chain of objects.

These patterns help in maintaining cleaner and more flexible code by promoting separation of concerns and reducing dependencies between objects.
