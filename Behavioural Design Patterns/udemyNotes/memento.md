# Memento Pattern

## Introduction
The Memento Pattern is a crucial behavioral design pattern that allows the state of an object to be saved and restored at a later time, enabling undo functionality.

## How Did We Get This Problem?
In applications where users need to revert to previous states (like text editors), managing current and past states can become complex. Storing state in multiple instances or directly exposing object attributes can lead to issues with data integrity and the inability to manage state transitions effectively.

## What Could've Been the Bad Solution?
A bad solution might involve:
- Storing the state directly within the main class (e.g., a text editor), allowing direct changes that can adversely affect the saved state.
- Not encapsulating the state, resulting in unintended alteration or inconsistent states when actions are performed.
- Creating different instances for each state which is inefficient and cumbersome.

## Why We Chose This Pattern?
The Memento Pattern promotes:
- Encapsulation: By using a separate Memento class, the internal state is hidden from the rest of the application, preserving the integrity of the state.
- Flexibility: Ensures that the original object (originator) does not need to manage its states, adhering to the Single Responsibility Principle (SRP).
- Easier Undo/Redo functionality: The pattern inherently supports restoring previous states.

## Example and Detailed Reasoning
### Example:
Consider a text editor application:
- **Originator**: TextEditor (handles editing).
- **Memento**: EditorMemento (stores the state).
- **Caretaker**: Caretaker (manages the memento for undo/redo).

### Use Case:
When a user edits a document:
1. **Save State**: Before making changes, the TextEditor saves its current state to an EditorMemento.
2. **Perform Edit**: The user modifies text. If they want to undo:
   - The Caretaker retrieves the appropriate memento and asks the TextEditor to restore its state.
   
This separation ensures that the TextEditor focuses solely on editing while the memento deals with state management, thus maintaining clean code and adherence to design principles.

## Conclusion
By using the Memento Pattern in applications requiring state management, we can enhance maintainability, flexibility, and adhere to software design principles efficiently.
