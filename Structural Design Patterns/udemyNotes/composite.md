### **Composite Pattern Notes**

#### **Overview of the Problem**

In systems that manage **hierarchical data** — such as file systems, organizational charts, or menus — handling both **individual items** and **groups of items** can become difficult. Developers often struggle to treat both single objects and collections of objects in a uniform way, leading to complex and redundant code.

#### **Bad Solution**

A poor approach is to create **separate classes and handling logic** for individual elements (like files) and composite elements (like folders).
This leads to:

* **Code duplication** (similar methods repeated across classes)
* **Complex logic** when dealing with mixed hierarchies
* **Reduced maintainability** and scalability

#### **Choosing the Composite Pattern**

The **Composite Pattern** solves this by allowing objects to be **composed into tree structures** that represent **part-whole hierarchies**.
This enables clients to treat **individual objects and groups uniformly**, simplifying the code and interaction model.

---

### **Example: Folder Structure Service**

#### **Scenario**

We want to represent a **file system** where folders can contain files and other folders.
The system should treat both files and folders using the same interface.

---

### **Code Implementation**

#### **1. Component Interface**

Defines a common interface for both **files** and **folders**.

```java
public interface FileSystemComponent {
    String getName();
    void show();
}
```

#### **2. Leaf Class (File)**

Represents individual file components — the “leaves” of the tree structure.

```java
public class FileLeaf implements FileSystemComponent {
    private String name;

    public FileLeaf(String name) {
        this.name = name;
    }

    @Override
    public String getName() {
        return name;
    }

    @Override
    public void show() {
        System.out.println("File: " + name);
    }
}
```

#### **3. Composite Class (Folder)**

Represents folders that can contain **files and/or other folders**.

```java
import java.util.ArrayList;
import java.util.List;

public class FolderComposite implements FileSystemComponent {
    private String name;
    private List<FileSystemComponent> components = new ArrayList<>();

    public FolderComposite(String name) {
        this.name = name;
    }

    public void add(FileSystemComponent component) {
        components.add(component);
    }

    public void remove(FileSystemComponent component) {
        components.remove(component);
    }

    @Override
    public String getName() {
        return name;
    }

    @Override
    public void show() {
        System.out.println("Folder: " + name);
        for (FileSystemComponent component : components) {
            component.show(); // Delegate to contained files/folders
        }
    }
}
```

---

### **Use Case**

This pattern is perfect for **tree-like structures**, such as:

* File systems
* Company hierarchies
* GUI components (buttons, panels, etc.)
* Document outlines

You can **add new component types** (like `ImageFile` or `VideoFile`) without changing existing code — aligning with the **Open/Closed Principle**.

#### **Example Usage**

```java
public class CompositePatternDemo {
    public static void main(String[] args) {
        FileLeaf file1 = new FileLeaf("document.txt");
        FileLeaf file2 = new FileLeaf("photo.jpg");

        FolderComposite folder1 = new FolderComposite("Documents");
        folder1.add(file1);
        folder1.add(file2);

        FolderComposite rootFolder = new FolderComposite("Root");
        rootFolder.add(folder1);
        rootFolder.add(new FileLeaf("readme.md"));

        rootFolder.show();
    }
}
```

**Output:**

```
Folder: Root
Folder: Documents
File: document.txt
File: photo.jpg
File: readme.md
```

---

### **Conclusion**

The **Composite Pattern** provides a unified way to handle both simple and complex (composite) objects in hierarchical systems.
It promotes:

* **Code simplicity** — one interface for all elements
* **Flexibility** — easy to extend and maintain
* **Consistency** — uniform treatment of files and folders

It’s an essential pattern for **hierarchical or recursive structures**, where part-whole relationships must be represented cleanly and efficiently.

---

Composite Pattern allows client code to interact with both individual objects and groups of objects through a unified interface, simplifying usage without requiring differentiation between the two. This aligns with the learning objective of understanding how the Composite Pattern streamlines the handling of complex tree structures in software design.

<img width="1166" height="826" alt="Composite_Pattern" src="https://github.com/user-attachments/assets/d625160b-267c-4b25-96b5-b437a5abd4e1" />
