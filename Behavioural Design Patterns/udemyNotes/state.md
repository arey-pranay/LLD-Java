# 🧩 State Pattern Notes

## 1. Understanding the Problem
The **State Pattern** is essential when an object's behavior changes based on its **internal state**.  
Without proper structure, managing multiple states can lead to **complex and unmanageable code**.

**Example:**  
In a **traffic light system**, the light’s behavior (`Red`, `Yellow`, `Green`) depends on its internal state.  
Each light state defines what happens next and how transitions occur dynamically.

---

## 2. Bad Solution
A common but problematic approach uses **long conditional statements** (`if-else` or `switch` blocks)  
to handle different states inside a **single class**.

**Problems with this approach:**
- Hard to read and maintain  
- Violates the **Single Responsibility Principle (SRP)**  
- Difficult to extend or modify behavior for new states  

```java
if (state == "RED") {
    // stop
} else if (state == "YELLOW") {
    // slow down
} else if (state == "GREEN") {
    // go
}
````

---

## 3. Choosing the State Pattern

The **State Pattern** solves these problems by:

* **Encapsulating each state** as a separate class
* Allowing a **context object** to reference a state object
* Promoting **modularity** and **extensibility**

**Benefits:**

* Adheres to **SOLID principles**:

  * **Single Responsibility Principle (SRP):** Each state has one purpose.
  * **Open/Closed Principle (OCP):** New states can be added without modifying existing code.
* Simplifies state transitions and behavior management.

---

## 4. Example and Detailed Reasoning

### Example: Ride-Sharing System

A ride can have multiple states:

* `Requested`
* `InProgress`
* `Completed`

Each state implements a **common interface** (e.g., `RideState`) defining actions like `proceed()` or `cancel()`.

```java
interface RideState {
    void proceed(RideContext context);
    void cancel(RideContext context);
}

class RequestedState implements RideState {
    public void proceed(RideContext context) {
        context.setState(new InProgressState());
    }
    public void cancel(RideContext context) {
        // Handle cancellation logic
    }
}

class InProgressState implements RideState {
    public void proceed(RideContext context) {
        context.setState(new CompletedState());
    }
    public void cancel(RideContext context) {
        // Can't cancel during in-progress
    }
}
```

The `RideContext` delegates behavior to its current state, enabling seamless transitions.

---

## 5. Use Case

**Digital Payment System Example:**
A transaction can have multiple states:

* `Initiated`
* `Processing`
* `Completed`
* `Failed`

Each state handles its specific logic — e.g., validation, notifications, or rollback — independently.

**Advantages:**

* Improves **scalability**
* Simplifies **debugging and maintenance**
* Makes transitions explicit and predictable

---

## ✅ Summary

| Aspect           | Without State Pattern  | With State Pattern     |
| ---------------- | ---------------------- | ---------------------- |
| Structure        | Long conditional logic | State-specific classes |
| Maintenance      | Hard to update         | Easy to extend         |
| SOLID Compliance | Violates SRP & OCP     | Follows SRP & OCP      |
| Readability      | Poor                   | Clear and modular      |

**Conclusion:**
The **State Pattern** provides a **clean, extensible, and robust** solution for managing objects whose behavior changes based on internal state — far superior to condition-heavy approaches.

<img width="1746" height="826" alt="State_Pattern" src="https://github.com/user-attachments/assets/34dd5ceb-dbe6-43e7-9ed8-96fff9cac3fb" />
