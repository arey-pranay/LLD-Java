# Template Method Pattern Notes

## Problem Statement
In software design, we often face situations where we need to define the skeleton of an algorithm in a base class but allow subclasses to provide specific implementations for certain steps. This situation arises when there are common procedures across multiple classes, yet variations exist that need to be implemented differently.

## Bad Solution
A common but ineffective solution is to implement the entire algorithm in each subclass. This leads to code duplication, making the system harder to maintain, more error-prone, and less flexible due to changing business requirements.

## Why We Chose This Pattern
The Template Method Pattern allows us to define the invariant parts of an algorithm once, while allowing subclasses to change the variant parts without replicating code. It promotes the DRY (Don’t Repeat Yourself) principle and makes the code easier to manage and extend.

## Example
Consider a scenario where we have a base class `DataParser` for parsing different data formats such as CSV, JSON, etc. The base class would implement the steps common to all parsers (like reading the file and closing the file), while each specific parser would implement the details (like parsing the content).

### Detailed Reasoning:
1. **Abstract Class**: Defines the template with concrete methods and an abstract method for the variable parts.
2. **Subclasses**: Implement the abstract method to provide format-specific behavior.
3. **Common Logic**: Shared logic remains in the abstract class, reducing redundancy and promoting a single source of truth.

## Use Case
This pattern is highly useful in frameworks where the framework defines the overarching processing structure, while the user can extend functionality by creating subclasses. For example, in a web framework, methods for handling requests might be templated, while actions based on routes could be handled by user-defined subclasses.

By employing the Template Method Pattern, we achieve a cleaner, more maintainable codebase that adheres to the principles of object-oriented design.

<img width="873" height="826" alt="Template_Pattern" src="https://github.com/user-attachments/assets/cca10c63-7eeb-4a25-b057-313e8858cdf2" />
