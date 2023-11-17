## Single Responsibility Principle
- A class should only contain functions that are needed for that particular function
## Open Close Principal
- Open for exntension closed fo modification
- This means make using of abstract clasees and extending them to change the implementation 
## Liskov Substitution Principle
- When we inherit from a parent class all methods get inherited in the child
- The problem arises when the child does not need all the methods instead only some 
- Solution is that the parent class should contain methods that are used by all child classes
## Interface Seggregation
- The class implmenting an interface should not be forced to implement all the interfaces that they do not use
- Have multiple interfaces
## Dependency Inversion
- Parent class should not directly rely on child class
- Instead we should have an interface that inverses the control 
- Because we can pass object by using interface refernce because of polymorphism
