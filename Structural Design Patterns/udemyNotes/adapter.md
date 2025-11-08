# Adapter Pattern Notes

## Problem Context
In this course section, we identified a problem where multiple services (like Driver and Passenger notifications) needed to be notified in a unified manner when events occur, particularly using a Notification Service.

## Bad Solution
A bad solution would have been to have each service (Driver and Passenger) directly handle notifications individually. This could lead to duplicated code and inconsistencies in how notifications are sent or formatted, making maintenance and updates difficult.

## Why We Chose the Adapter Pattern
The Adapter Pattern was chosen because it allows us to create a simplified interface to work with different notification services without changing how each individual component (Driver and Passenger) operates. It acts as a bridge to enable interaction between disparate systems seamlessly.

### Example: Notification Service

## Code Implementation

### Java

```java
// Notification interface
public interface Notification {
    void sendNotification(String message);
}

// EmailNotification implementation
public class EmailNotification implements Notification {
    @Override
    public void sendNotification(String message) {
        System.out.println("Email sent: " + message);
    }
}

// SMSNotification implementation
public class SMSNotification implements Notification {
    @Override
    public void sendNotification(String message) {
        System.out.println("SMS sent: " + message);
    }
}

// Adapter interface
public interface NotificationAdapter {
    void notifyUser(String message);
}

// Adapter for Email
public class EmailNotificationAdapter implements NotificationAdapter {
    private Notification emailNotification;

    public EmailNotificationAdapter(Notification emailNotification) {
        this.emailNotification = emailNotification;
    }

    @Override
    public void notifyUser(String message) {
        emailNotification.sendNotification(message);
    }
}

// Adapter for SMS
public class SMSNotificationAdapter implements NotificationAdapter {
    private Notification smsNotification;

    public SMSNotificationAdapter(Notification smsNotification) {
        this.smsNotification = smsNotification;
    }

    @Override
    public void notifyUser(String message) {
        smsNotification.sendNotification(message);
    }
}

// Usage
public class NotificationService {
    private List<NotificationAdapter> adapters = new ArrayList<>();

    public void addAdapter(NotificationAdapter adapter) {
        adapters.add(adapter);
    }

    public void sendNotification(String message) {
        for (NotificationAdapter adapter : adapters) {
            adapter.notifyUser(message);
        }
    }
}

// Example usage
public class Main {
    public static void main(String[] args) {
        NotificationService notificationService = new NotificationService();
        notificationService.addAdapter(new EmailNotificationAdapter(new EmailNotification()));
        notificationService.addAdapter(new SMSNotificationAdapter(new SMSNotification()));
        notificationService.sendNotification("Ride booked successfully!");
    }
}
````

## Detailed Reasoning

In this implementation:

* `Notification` is the base interface for sending notifications.
* `EmailNotification` and `SMSNotification` are concrete implementations that send messages in their respective ways.
* `NotificationAdapter` serves as the adapter interface, while `EmailNotificationAdapter` and `SMSNotificationAdapter` adapt the concrete implementations to the generic interface.
* `NotificationService` uses these adapters to send out notifications uniformly.

## Use Case

This pattern enables us to easily integrate new notification types in the future, such as push notifications, without altering existing code significantly, adhering to the Open/Closed Principle of SOLID principles.

<img width="1239" height="873" alt="Adapter_Pattern" src="https://github.com/user-attachments/assets/e2d97b78-4a3e-4077-ad18-fc38f668f326" />
