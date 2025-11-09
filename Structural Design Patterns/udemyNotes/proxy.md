### **Proxy Pattern Notes**

#### **Overview of the Problem**

In many applications, certain operations can be **resource-intensive**. For example, loading images from disk or from a network can take a significant amount of time and memory. Often, an image may not be displayed immediately, meaning loading it upfront could result in unnecessary resource consumption. This delay and wasted resources can impact application performance, especially in environments where resources are limited.

#### **Bad Solution**

A common but poor solution is to load resources directly in the main class that will display them. For example, each image object might load its corresponding image when created. This leads to problems like:

* **Wasted memory**: If the image is not displayed immediately, the system still consumes memory for the image.
* **Unnecessary delay**: Loading all images right away can delay the initial application startup, even if the user never interacts with those images.

#### **Choosing the Proxy Pattern**

The **Proxy Pattern** addresses these issues by introducing a **proxy** class that acts as a placeholder for the real resource. The proxy class can **delay** resource loading until it is actually needed (known as **lazy loading**). In addition to lazy loading, the proxy can also manage other concerns like caching, access control, and logging, without modifying the core functionality of the real resource class.

### **Example: Image Load Service**

#### **Scenario**

Imagine a service that handles the loading and display of images. Given that image loading can be a **resource-heavy** operation, it’s inefficient to load all images at once. Instead, we can use the **Proxy Pattern** to load images only when they are actually displayed.

---

### **Code Implementation**

#### **1. Image Interface**

The `Image` interface defines the basic contract for displaying images.

```java
public interface Image {
    void display();
}
```

#### **2. RealImage Class**

The `RealImage` class is responsible for actually loading and displaying the image. This class simulates a **resource-intensive operation** (such as reading an image from disk).

```java
public class RealImage implements Image {
    private String filename;

    public RealImage(String filename) {
        this.filename = filename;
        loadImageFromDisk(); // Simulate resource-intensive operation
    }

    private void loadImageFromDisk() {
        System.out.println("Loading " + filename); // Simulate disk I/O
    }

    @Override
    public void display() {
        System.out.println("Displaying " + filename); // Simulate displaying the image
    }
}
```

#### **3. ProxyImage Class**

The `ProxyImage` class controls access to the `RealImage` class and implements **lazy loading**. The image is only loaded when the `display()` method is called for the first time.

```java
public class ProxyImage implements Image {
    private RealImage realImage;
    private String filename;

    public ProxyImage(String filename) {
        this.filename = filename;
    }

    @Override
    public void display() {
        // Load image only if it hasn't been loaded yet
        if (realImage == null) {
            realImage = new RealImage(filename); // Lazy loading of the real image
        }
        realImage.display();
    }
}
```

---

### **Use Case**

The **Proxy Pattern** is particularly useful when dealing with **resource-heavy operations** like loading large images or files. By using a proxy, you can ensure that resources are loaded only when necessary, thereby improving application performance and memory usage.

#### **Example Usage:**

```java
public class ProxyPatternTest {
    public static void main(String[] args) {
        Image image1 = new ProxyImage("image1.jpg");
        Image image2 = new ProxyImage("image2.jpg");

        // Image is loaded and displayed only when requested
        image1.display();  // First time access, image is loaded
        image1.display();  // Image is not loaded again, just displayed

        image2.display();  // Image is loaded only when requested
    }
}
```

**Output:**

```
Loading image1.jpg
Displaying image1.jpg
Displaying image1.jpg
Loading image2.jpg
Displaying image2.jpg
```

---

### **Conclusion**

The **Proxy Pattern** is an effective way to **manage resource-intensive operations** like loading images, files, or other components that may not be needed immediately. By using a proxy, you can achieve **lazy loading**, **caching**, and **access control**, which helps improve performance and resource management.

* **Lazy loading**: Resources are only loaded when needed.
* **Memory optimization**: Reduces memory consumption by delaying resource loading.
* **Separation of concerns**: The proxy class takes care of resource management without modifying the core logic of the real resource class.

This pattern ensures that your application remains responsive and efficient by delaying the loading of resources until they are actually needed.

<img width="1166" height="826" alt="Proxy_Pattern" src="https://github.com/user-attachments/assets/c1c51bde-da0a-46d9-a7a0-f8fefc500929" />

