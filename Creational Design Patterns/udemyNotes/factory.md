# Factory Pattern Notes

## Problem Overview
In software design, there's often a need to create objects without specifying the exact class of the object that will be created. This is particularly important in scenarios where the creation process might be complex or when we work with different variations of a certain type of object.

## Bad Solution
One common bad solution is to use a series of conditional statements (like if-else or switch-case) to determine which object to create. While this method might seem straightforward, it quickly becomes unmanageable and violates the **Open/Closed Principle**, as adding new types requires modifying existing code.

## Why We Chose This Pattern
The Factory Pattern helps to encapsulate the object creation logic, allowing the code to be more flexible and maintainable. By utilizing a factory, we enable the application to be extended without altering existing code, thus adhering to **SOLID** principles. This design promotes a separation of concerns, which is essential for scalable applications.

## Example

### Example Code (Java)

```java
public interface Transport {
    void deliver();
}

public class Truck implements Transport {
    @Override
    public void deliver() {
        System.out.println("Delivering by truck.");
    }
}

public class Ship implements Transport {
    @Override
    public void deliver() {
        System.out.println("Delivering by ship.");
    }
}

public class TransportFactory {
    public static Transport createTransport(String type) {
        switch(type) {
            case "Truck":
                return new Truck();
            case "Ship":
                return new Ship();
            default:
                throw new IllegalArgumentException("Unknown transport type");
        }
    }
}
````

### Detailed Reasoning

* The `TransportFactory` class creates objects based on the type specified. This reduces the dependency on specific classes and enhances code reusability.
* The use of an interface (`Transport`) allows for easy expansion of future implementations without altering existing factory logic.

## Use Case

A practical use case for the Factory Pattern can be seen in logistics applications. If an application needs to manage different transport types (e.g., trucks and ships), employing a factory to create these transport objects simplifies the process of adding new transport types while keeping the system extensible. Should a new transport class be required (e.g., a **Plane**), it can be added without changing the existing factory structure, maintaining system robustness and clarity.

---


<img width="1239" height="873" alt="Factory_Pattern" src="https://github.com/user-attachments/assets/5eefacc2-4f29-4af5-a03e-f7f7fadf2826" />
