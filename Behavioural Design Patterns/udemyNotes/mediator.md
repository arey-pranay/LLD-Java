# 🧩 Mediator Pattern Notes

## 1. Problem Introduction

In a system where multiple objects (e.g., drivers and passengers) need to communicate with each other, direct interactions can lead to a complex set of dependencies.
This makes it difficult to manage and modify the system.

---

## 2. Bad Solution

A potential bad solution would be to allow all objects to communicate directly with one another.
This approach can lead to:

* ⚠️ Increased coupling between objects, making them dependent on each other.
* ⚠️ Complicated maintenance or extensions of the system.
* ⚠️ The addition of new object types requiring changes in multiple classes instead of a single coordination point.

---

## 3. Choosing the Mediator Pattern

The **Mediator Pattern** helps reduce the complexity of communication.
By introducing a mediator, we can:

* 🧠 **Encapsulate** the interaction logic between objects.
* 🔗 **Maintain loose coupling**, as objects do not need to know about each other.
* 🧩 **Simplify interactions**, as each object only knows about the mediator, not each other.

---

## 4. Example and Detailed Reasoning

### Scenario

Imagine a **ride-matching system** where the mediator class manages communication between **drivers** and **passengers**.

### Example Structure

* **Mediator:** `RideMatcher`
* **Colleagues:** `Driver` and `Passenger` classes that interact with the `RideMatcher`.

### Functionality

* When a passenger requests a ride, the `RideMatcher` finds the nearest driver and notifies both parties about the ride details.
* The `RideMatcher` contains methods such as:

  * `requestRide()`
  * `findNearestDriver()`

✅ This design significantly reduces code complexity compared to direct communication between drivers and passengers.

---

## 5. Use Case

In a **ride-sharing application**:

* The `RideMatcher` acts as a **central hub** that handles all notifications and requests.
* It **separates concerns**:

  * `RideMatcher` manages ride coordination.
  * `Driver` and `Passenger` handle their own specific logic.

This design follows the **Single Responsibility Principle (SRP)**:

* `RideMatcher` → manages rides.
* `Driver` / `Passenger` → handle their own responsibilities.

---

## ✅ Benefits of the Mediator Pattern

* Reduced coupling between classes.
* Easier maintenance and scalability.
* Centralized management of complex communication logic.
* Simpler extension when adding new participant types.


<img width="1455" height="826" alt="Mediator_Pattern" src="https://github.com/user-attachments/assets/8aba01ac-0a0d-4015-909f-720cdcecd666" />
