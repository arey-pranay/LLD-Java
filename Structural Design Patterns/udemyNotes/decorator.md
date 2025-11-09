### **Decorator Pattern Notes**

#### **Overview of the Problem**

In typical application development, adding new functionalities dynamically can be challenging. As new features are added, the code often becomes harder to manage, as modifying existing classes can unintentionally introduce bugs. A common issue arises when developers need to extend a class with new features, leading to fragile, inflexible code.

#### **Bad Solution**

A typical poor solution is **subclassing**, where developers create multiple subclasses to handle different combinations of features. This can lead to a **class explosion**, where there are so many variations of the same class that the codebase becomes hard to navigate and maintain.

#### **Choosing the Decorator Pattern**

The **Decorator Pattern** allows you to add functionality to objects dynamically without altering their class structure. This pattern provides better code organization and flexibility by enabling you to **mix and match** functionalities at runtime. It avoids the need for subclassing and prevents the proliferation of classes, leading to a more maintainable and extensible codebase.

### **Example: Pizza Service**

#### **Scenario**

Consider a pizza service where customers can customize their pizzas with various toppings like cheese, olives, or pepperoni. Using the Decorator Pattern, we can dynamically add toppings without changing the underlying pizza classes.

---

### **Code Implementation**

#### **1. Pizza Interface**

The `Pizza` interface defines the core methods that any pizza must implement.

```java
public interface Pizza {
    String getDescription();
    double getCost();
}
```

#### **2. Concrete Pizza Classes**

The concrete pizza classes represent specific types of pizza (e.g., Margherita Pizza) that implement the `Pizza` interface.

```java
public class MargheritaPizza implements Pizza {
    @Override
    public String getDescription() {
        return "Margherita Pizza";
    }

    @Override
    public double getCost() {
        return 8.00; // Base cost for Margherita Pizza
    }
}
```

#### **3. Decorator Class**

The `PizzaDecorator` class is abstract and implements the `Pizza` interface. It contains a reference to a `Pizza` object and delegates calls to the wrapped pizza. This ensures that the decorator follows the same contract as the original pizza.

```java
public abstract class PizzaDecorator implements Pizza {
    protected Pizza pizza;

    public PizzaDecorator(Pizza pizza) {
        this.pizza = pizza;
    }
}
```

#### **4. Concrete Decorator Classes**

These classes extend `PizzaDecorator` and add specific toppings to the pizza.

* **CheeseDecorator**: Adds cheese as a topping to the pizza.

```java
public class CheeseDecorator extends PizzaDecorator {
    public CheeseDecorator(Pizza pizza) {
        super(pizza);
    }

    @Override
    public String getDescription() {
        return pizza.getDescription() + ", Cheese";
    }

    @Override
    public double getCost() {
        return pizza.getCost() + 1.50; // Additional cost for cheese
    }
}
```

* **OliveDecorator**: Adds olives as a topping to the pizza.

```java
public class OliveDecorator extends PizzaDecorator {
    public OliveDecorator(Pizza pizza) {
        super(pizza);
    }

    @Override
    public String getDescription() {
        return pizza.getDescription() + ", Olives";
    }

    @Override
    public double getCost() {
        return pizza.getCost() + 0.75; // Additional cost for olives
    }
}
```

---

### **Use Case**

The **Decorator Pattern** is particularly useful when you want to add or modify the behavior of an object without changing its structure. In this example, the `Pizza` interface allows you to create a basic pizza (e.g., Margherita), and then add toppings dynamically using decorators. You can apply as many decorators as needed to create custom pizza combinations.

#### **Example Usage:**

```java
Pizza myPizza = new MargheritaPizza();
System.out.println(myPizza.getDescription() + " Cost: $" + myPizza.getCost());

myPizza = new CheeseDecorator(myPizza);
System.out.println(myPizza.getDescription() + " Cost: $" + myPizza.getCost());

myPizza = new OliveDecorator(myPizza);
System.out.println(myPizza.getDescription() + " Cost: $" + myPizza.getCost());
```

**Output:**

```
Margherita Pizza Cost: $8.00
Margherita Pizza, Cheese Cost: $9.50
Margherita Pizza, Cheese, Olives Cost: $10.25
```

---

### **Conclusion**

The **Decorator Pattern** is an effective way to enhance or modify the behavior of an object without changing its core structure. It allows you to add functionalities dynamically and avoid the drawbacks of subclassing, such as class explosion and rigid code.

<img width="1239" height="873" alt="Decorator_Pattern" src="https://github.com/user-attachments/assets/8e476c43-1b2d-4cc1-8627-001a5843a344" />

