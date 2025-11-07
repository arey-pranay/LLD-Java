## **Builder Pattern**

### **How Did We Get This Problem?**

The **Builder Pattern** emerged to address the challenges of constructing complex objects that require multiple parts and configurations.
When objects have numerous attributes, traditional constructors can become cluttered and difficult to maintain — especially as variations or optional parameters increase.

### **What Could Have Been the Bad Solution?**

A naive approach would be to use a single constructor with many parameters or multiple overloaded constructors.
However, this can lead to several issues:

* **Constructor Overloading**: Creating different constructors for each variation makes the code complex and less readable.
* **Immutability Issues**: Using fixed attributes restricts flexibility; modifying one attribute might require reconstructing the entire object.
* **Poor Maintainability**: Increasing the number of parameters complicates updates and introduces the risk of errors when extending functionality.

### **Why We Chose This Pattern**

The **Builder Pattern** offers several key advantages:

* **Step-by-Step Construction**: Objects can be constructed gradually through a sequence of defined steps, improving clarity and flexibility.
* **Separation of Construction and Representation**: The pattern separates the object creation logic (builder) from the representation (product), enhancing maintainability.
* **Ease of Modification**: Changes to object components can be implemented easily without affecting other parts of the construction process.

---

### **Example with Code**

Let’s illustrate the **Builder Pattern** using an example of constructing a `House` object.

#### **Java Implementation**

```java
// Product
class House {
    private String foundation;
    private String structure;
    private String roof;

    public void setFoundation(String foundation) { this.foundation = foundation; }
    public void setStructure(String structure) { this.structure = structure; }
    public void setRoof(String roof) { this.roof = roof; }
}
```

```java
// Builder Interface
interface HouseBuilder {
    void buildFoundation();
    void buildStructure();
    void buildRoof();
    House getHouse();
}
```

```java
// Concrete Builder
class WoodenHouseBuilder implements HouseBuilder {
    private House house = new House();

    public void buildFoundation() { house.setFoundation("Wooden Foundation"); }
    public void buildStructure() { house.setStructure("Wooden Structure"); }
    public void buildRoof() { house.setRoof("Wooden Roof"); }
    public House getHouse() { return house; }
}
```

```java
// Director
class ConstructionEngineer {
    private HouseBuilder builder;

    public ConstructionEngineer(HouseBuilder builder) { this.builder = builder; }

    public House constructHouse() {
        builder.buildFoundation();
        builder.buildStructure();
        builder.buildRoof();
        return builder.getHouse();
    }
}
```

---

### **Detailed Reasoning**

* **Product Class (`House`)**: Represents the complex object being built, containing multiple configurable parts (foundation, structure, roof).
* **Builder Interface**: Defines the abstract steps required to construct a product.
* **Concrete Builder (`WoodenHouseBuilder`)**: Provides specific implementations of the building process for a particular type of product.
* **Director (`ConstructionEngineer`)**: Orchestrates the construction sequence, ensuring the product is built correctly and consistently.

---

### **Use Case**

The **Builder Pattern** is particularly useful in scenarios where objects have multiple components or configurations, such as:

* Constructing **complex objects** like houses, vehicles, or meals.
* Building **objects with optional attributes**, where not all parameters are required at once.
* **Simplifying creation logic** in systems that need flexibility for future enhancements or variations.

By applying the Builder Pattern, developers can simplify object construction, improve readability, and maintain a high degree of flexibility for future changes.


<img width="1007" height="574" alt="image" src="https://github.com/user-attachments/assets/671eed9a-3457-43d0-a6a5-6d11b8471470" />

---

<img width="1167" height="1240" alt="Builder_Pattern" src="https://github.com/user-attachments/assets/953cf511-e4bd-4927-b9c7-c5fe8a00d6d2" />

