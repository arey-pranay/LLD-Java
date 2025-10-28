# Observer Pattern Notes

## How Did We Get This Problem?
The observer pattern addresses situations where one object, known as the **subject**, needs to notify multiple dependent objects, known as **observers**, about changes in state.  
In applications like **ride-sharing**, both drivers and passengers need real-time updates regarding the ride status.

## What Could've Been the Bad Solution?
A bad solution might involve **hard-coding notifications** for each observer directly within the subject.  
This leads to **tight coupling** between the subject and observers, complicating maintenance and scalability.  
It becomes cumbersome to manage observers as the number of notifications increases, opening up possibilities for **memory leaks** and making the system **fragile**.

## Why We Chose This Pattern
The **observer pattern** promotes **loose coupling**.  
By allowing observers to **subscribe** to a subject, the observers can react to changes without the subject needing to know specifics about them.  
This aids in maintaining the system, following the **Single Responsibility Principle (SRP)**, and ensuring that components can evolve independently.

## Example
Consider a **ride-sharing application**:

- **Subject:** `RideScheduler` – manages the scheduling of rides and notifies registered observers.  
- **Observers:** `Driver` and `Passenger` classes implement a `notify()` method to receive updates.

## Detailed Reasoning
In this implementation, `RideScheduler` maintains a **list of observers** (both drivers and passengers) and uses the `notify()` method to inform them of any **ride status changes**, such as ride acceptance or cancellation.  
This allows for **flexible handling of notifications** based on the type of observer while maintaining a **clean code structure**.

## Use Case
A practical scenario for the observer pattern can be seen in **social media applications**, where a user posting an update should notify all followers.  
It serves well in any situation requiring **real-time updates**, making it widely applicable for systems with **dynamic observer lists**.


<img width="1455" height="826" alt="Observer_Pattern" src="https://github.com/user-attachments/assets/25207b5e-bf10-4060-987b-50560004c6c8" />
