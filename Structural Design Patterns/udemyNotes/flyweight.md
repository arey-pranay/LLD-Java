## **Flyweight Pattern Notes**

### **Overview of the Problem**

In applications that create **large numbers of similar objects**, such as games or graphics programs, memory usage can quickly become excessive.
When many objects share similar properties or behavior, storing duplicate data across all instances leads to **inefficient memory usage** and degraded performance.

---

### **Bad Solution**

A naive approach would be to create a **separate instance for every object**, even when many objects share identical data.

**Problems with this approach:**

* **Excessive memory consumption** due to redundant data.
* **Poor scalability** — the system struggles to handle large numbers of objects.
* **Reduced performance**, especially in memory-constrained environments.

---

### **Choosing the Flyweight Pattern**

The **Flyweight Pattern** provides a solution by **sharing common (intrinsic) data** across multiple objects while keeping **unique (extrinsic) data** external to the shared objects.

This pattern allows applications to:

* **Reduce memory usage** by sharing immutable, reusable objects.
* **Maintain scalability**, as fewer unique instances are created.
* **Improve performance** in systems with high object counts.

**Key Concept:**

* **Intrinsic state** → Shared data common to all objects (e.g., color, shape).
* **Extrinsic state** → Unique data specific to each instance (e.g., position, speed).

---

## **Example: Game Shooting Service**

### **Scenario**

In a shooting game, many bullets may exist simultaneously. While each bullet differs in position or direction, they share common properties like **color, texture, or shape**.
Using the **Flyweight Pattern**, we can share the common attributes to reduce memory usage.

---

### **Code Implementation**

#### **1. Flyweight Interface**

Defines a shared interface that all bullet objects must implement.

```java
public interface Bullet {
    void shoot(String position);
}
```

---

#### **2. Concrete Flyweight Class**

Represents the shared, intrinsic state of the bullet (e.g., color).

```java
public class ConcreteBullet implements Bullet {
    private String color; // Intrinsic state

    public ConcreteBullet(String color) {
        this.color = color;
    }

    @Override
    public void shoot(String position) {
        System.out.println("Shooting a " + color + " bullet at " + position);
    }
}
```

---

#### **3. Flyweight Factory**

Manages shared instances of bullets. It ensures that only one object is created per color.

```java
import java.util.HashMap;
import java.util.Map;

public class BulletFactory {
    private Map<String, Bullet> bullets = new HashMap<>();

    public Bullet getBullet(String color) {
        Bullet bullet = bullets.get(color);
        if (bullet == null) {
            bullet = new ConcreteBullet(color);
            bullets.put(color, bullet);
        }
        return bullet;
    }
}
```

---

#### **4. Client Code**

Uses the factory to obtain and reuse bullet instances efficiently.

```java
public class Game {
    private BulletFactory bulletFactory = new BulletFactory();

    public void shootBullet(String color, String position) {
        Bullet bullet = bulletFactory.getBullet(color);
        bullet.shoot(position);
    }

    public static void main(String[] args) {
        Game game = new Game();

        game.shootBullet("Red", "Position A");
        game.shootBullet("Red", "Position B");
        game.shootBullet("Blue", "Position C");
        game.shootBullet("Red", "Position D");
    }
}
```

**Output:**

```
Shooting a Red bullet at Position A
Shooting a Red bullet at Position B
Shooting a Blue bullet at Position C
Shooting a Red bullet at Position D
```

---

### **Use Case**

The **Flyweight Pattern** is particularly beneficial when working with applications that involve **large quantities of similar objects**, such as:

* Game elements (bullets, enemies, particles)
* Character rendering in text editors or graphic engines
* Caching systems where shared data is reused frequently

By sharing intrinsic data, systems can:

* **Greatly reduce memory usage**
* **Improve object creation speed**
* **Scale efficiently**, even with thousands of active objects

---

### **Conclusion**

The **Flyweight Pattern** is a **structural design pattern** that focuses on **memory optimization through object sharing**.
It separates shared and unique state to reduce redundancy and enable large-scale object management efficiently.

**Benefits:**

* Efficient memory usage
* Reduced object creation overhead
* Improved scalability and performance

**Trade-offs:**

* Slightly increased complexity in managing extrinsic data
* May require additional logic for maintaining object state consistency

--- 

<img width="826" height="873" alt="FlyWeight_Pattern" src="https://github.com/user-attachments/assets/0a71a46c-b1d5-4a48-a465-ecac64a122b1" />

