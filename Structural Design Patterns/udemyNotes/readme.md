# 🏛️ Structural Design Patterns in Java

**Structural Design Patterns** deal with object composition and typically identify simple ways to realize relationships between different objects.

---

## 📚 Overview

**Definition:** Structural patterns explain how to assemble objects and classes into larger structures while keeping these structures flexible and efficient.

**Purpose:**

* Simplify structure by identifying relationships
* Compose objects to form larger structures
* Ensure flexibility and efficiency in design

---

## 🔌 1. Adapter Pattern

**Definition**: Converts the interface of a class into another interface that clients expect, allowing incompatible interfaces to work together.

**Use Case**: Integrating legacy code, third-party libraries, payment gateways.

**Java Example**:

```java
// Target interface
interface MediaPlayer {
    void play(String audioType, String fileName);
}

// Adaptee (incompatible interface)
class AdvancedMediaPlayer {
    public void playVlc(String fileName) {
        System.out.println("Playing vlc file: " + fileName);
    }
    
    public void playMp4(String fileName) {
        System.out.println("Playing mp4 file: " + fileName);
    }
}

// Adapter
class MediaAdapter implements MediaPlayer {
    AdvancedMediaPlayer advancedPlayer;
    
    public MediaAdapter(String audioType) {
        advancedPlayer = new AdvancedMediaPlayer();
    }
    
    public void play(String audioType, String fileName) {
        if (audioType.equals("vlc")) {
            advancedPlayer.playVlc(fileName);
        } else if (audioType.equals("mp4")) {
            advancedPlayer.playMp4(fileName);
        }
    }
}

// Client
class AudioPlayer implements MediaPlayer {
    MediaAdapter mediaAdapter;
    
    public void play(String audioType, String fileName) {
        if (audioType.equals("mp3")) {
            System.out.println("Playing mp3 file: " + fileName);
        } else if (audioType.equals("vlc") || audioType.equals("mp4")) {
            mediaAdapter = new MediaAdapter(audioType);
            mediaAdapter.play(audioType, fileName);
        }
    }
}
```

**📌 Intent**: Bridge the gap between incompatible interfaces.

**🧠 When to Use**:

* You want to use an existing class but its interface doesn't match what you need
* You need to integrate legacy or third-party code
* You want to create reusable classes that cooperate with unrelated classes

**✅ Benefits**:

* Increases reusability of existing code
* Promotes single responsibility principle
* Allows integration without modifying existing code

---

## 🌉 2. Bridge Pattern

**Definition**: Decouples an abstraction from its implementation so that the two can vary independently.

**Use Case**: GUI frameworks, device drivers, database drivers.

**Java Example**:

```java
// Implementor
interface Device {
    void turnOn();
    void turnOff();
}

// Concrete Implementors
class TV implements Device {
    public void turnOn() {
        System.out.println("TV is ON");
    }
    
    public void turnOff() {
        System.out.println("TV is OFF");
    }
}

class Radio implements Device {
    public void turnOn() {
        System.out.println("Radio is ON");
    }
    
    public void turnOff() {
        System.out.println("Radio is OFF");
    }
}

// Abstraction
abstract class RemoteControl {
    protected Device device;
    
    public RemoteControl(Device device) {
        this.device = device;
    }
    
    abstract void togglePower();
}

// Refined Abstraction
class BasicRemote extends RemoteControl {
    public BasicRemote(Device device) {
        super(device);
    }
    
    public void togglePower() {
        System.out.println("Basic Remote:");
        device.turnOn();
    }
}

class AdvancedRemote extends RemoteControl {
    public AdvancedRemote(Device device) {
        super(device);
    }
    
    public void togglePower() {
        System.out.println("Advanced Remote:");
        device.turnOn();
    }
    
    public void mute() {
        System.out.println("Device muted");
    }
}
```

**📌 Intent**: Separate abstraction from implementation to allow independent variation.

**🧠 When to Use**:

* You want to avoid permanent binding between abstraction and implementation
* Both abstractions and implementations should be extensible by subclassing
* Changes in implementation should not affect clients

**✅ Benefits**:

* Decouples interface from implementation
* Improves extensibility
* Hides implementation details from clients

---

## 🎄 3. Composite Pattern

**Definition**: Composes objects into tree structures to represent part-whole hierarchies, allowing clients to treat individual objects and compositions uniformly.

**Use Case**: File systems, organization hierarchies, UI components.

**Java Example**:

```java
import java.util.ArrayList;
import java.util.List;

// Component
interface Employee {
    void showDetails();
}

// Leaf
class Developer implements Employee {
    private String name;
    private String position;
    
    public Developer(String name, String position) {
        this.name = name;
        this.position = position;
    }
    
    public void showDetails() {
        System.out.println(name + " - " + position);
    }
}

// Composite
class Manager implements Employee {
    private String name;
    private String position;
    private List<Employee> employees = new ArrayList<>();
    
    public Manager(String name, String position) {
        this.name = name;
        this.position = position;
    }
    
    public void addEmployee(Employee emp) {
        employees.add(emp);
    }
    
    public void removeEmployee(Employee emp) {
        employees.remove(emp);
    }
    
    public void showDetails() {
        System.out.println(name + " - " + position);
        for (Employee emp : employees) {
            emp.showDetails();
        }
    }
}
```

**📌 Intent**: Treat individual objects and compositions of objects uniformly.

**🧠 When to Use**:

* You need to represent part-whole hierarchies
* You want clients to ignore the difference between compositions and individual objects
* You're working with tree structures

**✅ Benefits**:

* Simplifies client code
* Makes it easier to add new components
* Provides flexibility in structure

---

## 🎨 4. Decorator Pattern

**Definition**: Attaches additional responsibilities to an object dynamically, providing a flexible alternative to subclassing for extending functionality.

**Use Case**: Adding features to GUI components, stream processing, pizza toppings.

**Java Example**:

```java
// Component
interface Coffee {
    String getDescription();
    double getCost();
}

// Concrete Component
class SimpleCoffee implements Coffee {
    public String getDescription() {
        return "Simple Coffee";
    }
    
    public double getCost() {
        return 2.0;
    }
}

// Decorator
abstract class CoffeeDecorator implements Coffee {
    protected Coffee coffee;
    
    public CoffeeDecorator(Coffee coffee) {
        this.coffee = coffee;
    }
    
    public String getDescription() {
        return coffee.getDescription();
    }
    
    public double getCost() {
        return coffee.getCost();
    }
}

// Concrete Decorators
class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }
    
    public String getDescription() {
        return coffee.getDescription() + ", Milk";
    }
    
    public double getCost() {
        return coffee.getCost() + 0.5;
    }
}

class SugarDecorator extends CoffeeDecorator {
    public SugarDecorator(Coffee coffee) {
        super(coffee);
    }
    
    public String getDescription() {
        return coffee.getDescription() + ", Sugar";
    }
    
    public double getCost() {
        return coffee.getCost() + 0.3;
    }
}
```

**📌 Intent**: Add responsibilities to objects dynamically without altering their structure.

**🧠 When to Use**:

* You want to add responsibilities to individual objects dynamically
* Extension by subclassing is impractical
* You need to add features that can be withdrawn

**✅ Benefits**:

* More flexible than static inheritance
* Avoids feature-laden classes high in the hierarchy
* Responsibilities can be added or removed at runtime

---

## 🎭 5. Facade Pattern

**Definition**: Provides a unified interface to a set of interfaces in a subsystem, making the subsystem easier to use.

**Use Case**: Complex library APIs, multimedia frameworks, database access layers.

**Java Example**:

```java
// Complex subsystem classes
class CPU {
    public void freeze() {
        System.out.println("CPU: Freezing...");
    }
    
    public void jump(long position) {
        System.out.println("CPU: Jumping to " + position);
    }
    
    public void execute() {
        System.out.println("CPU: Executing...");
    }
}

class Memory {
    public void load(long position, byte[] data) {
        System.out.println("Memory: Loading data at " + position);
    }
}

class HardDrive {
    public byte[] read(long lba, int size) {
        System.out.println("HardDrive: Reading " + size + " bytes from " + lba);
        return new byte[size];
    }
}

// Facade
class ComputerFacade {
    private CPU cpu;
    private Memory memory;
    private HardDrive hardDrive;
    
    public ComputerFacade() {
        this.cpu = new CPU();
        this.memory = new Memory();
        this.hardDrive = new HardDrive();
    }
    
    public void start() {
        System.out.println("Computer starting...");
        cpu.freeze();
        memory.load(0, hardDrive.read(0, 1024));
        cpu.jump(0);
        cpu.execute();
        System.out.println("Computer started!");
    }
}
```

**📌 Intent**: Simplify complex subsystems by providing a simple interface.

**🧠 When to Use**:

* You want to provide a simple interface to a complex subsystem
* There are many dependencies between clients and implementation classes
* You want to layer your subsystems

**✅ Benefits**:

* Shields clients from subsystem complexity
* Promotes weak coupling
* Easier to use and understand

---

## 🪶 6. Flyweight Pattern

**Definition**: Uses sharing to support large numbers of fine-grained objects efficiently by sharing common state.

**Use Case**: Text editors (character objects), game development (particles, bullets), caching.

**Java Example**:

```java
import java.util.HashMap;
import java.util.Map;

// Flyweight
class TreeType {
    private String name;
    private String color;
    private String texture;
    
    public TreeType(String name, String color, String texture) {
        this.name = name;
        this.color = color;
        this.texture = texture;
    }
    
    public void draw(int x, int y) {
        System.out.println("Drawing " + name + " tree at (" + x + "," + y + 
                         ") with color " + color);
    }
}

// Flyweight Factory
class TreeFactory {
    private static Map<String, TreeType> treeTypes = new HashMap<>();
    
    public static TreeType getTreeType(String name, String color, String texture) {
        String key = name + color + texture;
        if (!treeTypes.containsKey(key)) {
            treeTypes.put(key, new TreeType(name, color, texture));
            System.out.println("Creating new tree type: " + name);
        }
        return treeTypes.get(key);
    }
}

// Context
class Tree {
    private int x;
    private int y;
    private TreeType type;
    
    public Tree(int x, int y, TreeType type) {
        this.x = x;
        this.y = y;
        this.type = type;
    }
    
    public void draw() {
        type.draw(x, y);
    }
}

// Forest (Client)
class Forest {
    private List<Tree> trees = new ArrayList<>();
    
    public void plantTree(int x, int y, String name, String color, String texture) {
        TreeType type = TreeFactory.getTreeType(name, color, texture);
        Tree tree = new Tree(x, y, type);
        trees.add(tree);
    }
    
    public void draw() {
        for (Tree tree : trees) {
            tree.draw();
        }
    }
}
```

**📌 Intent**: Minimize memory usage by sharing data among similar objects.

**🧠 When to Use**:

* Application uses a large number of objects
* Storage costs are high due to quantity of objects
* Most object state can be made extrinsic (shared)
* Groups of objects can be replaced by relatively few shared objects

**✅ Benefits**:

* Reduces memory consumption
* Improves performance for large numbers of objects
* Centralizes state management

---

## 🔍 7. Proxy Pattern

**Definition**: Provides a surrogate or placeholder for another object to control access to it.

**Use Case**: Lazy initialization, access control, logging, caching, remote objects.

**Java Example**:

```java
// Subject
interface Image {
    void display();
}

// Real Subject
class RealImage implements Image {
    private String fileName;
    
    public RealImage(String fileName) {
        this.fileName = fileName;
        loadFromDisk();
    }
    
    private void loadFromDisk() {
        System.out.println("Loading image: " + fileName);
    }
    
    public void display() {
        System.out.println("Displaying image: " + fileName);
    }
}

// Proxy
class ProxyImage implements Image {
    private String fileName;
    private RealImage realImage;
    
    public ProxyImage(String fileName) {
        this.fileName = fileName;
    }
    
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(fileName);
        }
        realImage.display();
    }
}
```

**📌 Intent**: Control access to an object by providing a surrogate.

**🧠 When to Use**:

* You need lazy initialization (virtual proxy)
* You need access control (protection proxy)
* You need to add functionality before/after accessing an object
* You're working with remote objects (remote proxy)

**✅ Benefits**:

* Controls access to the original object
* Can provide additional functionality
* Supports lazy loading and caching

---

## 📊 Summary Table

| Pattern       | Use Case Example           | Intent                               | Key Benefit                        |
| ------------- | -------------------------- | ------------------------------------ | ---------------------------------- |
| **Adapter**   | Payment gateway integration| Make incompatible interfaces work    | Reuses existing code               |
| **Bridge**    | Device drivers             | Separate abstraction from implementation | Independent variation           |
| **Composite** | File system hierarchy      | Treat individual/composite uniformly | Simplifies client code             |
| **Decorator** | Coffee with toppings       | Add responsibilities dynamically     | Flexible alternative to subclassing|
| **Facade**    | Computer startup           | Simplify complex subsystems          | Easy-to-use interface              |
| **Flyweight** | Text editor characters     | Share common state efficiently       | Reduces memory footprint           |
| **Proxy**     | Image lazy loading         | Control access to objects            | Adds control layer                 |
