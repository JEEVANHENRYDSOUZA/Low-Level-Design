## Relationship Between Classes
### Introduction
- Broadly there are two types of relationship
    1. Is-A relationship
    2. Has-A relationship
### Is-a relationship
- Is-a relationship is also called as inheritance
1. **Superclass and Subclass:** Inheritance involves two types of classes:
   - **Superclass (Base Class or Parent Class):** This is the existing class whose attributes and behaviors you want to reuse.
   - **Subclass (Derived Class or Child Class):** This is the new class that you create by inheriting from the superclass. It can have its attributes and behaviors in addition to those inherited from the superclass.

2. **Syntax:** To create a subclass in Java, you use the `extends` keyword. For example:
   ```java
   class Subclass extends Superclass {
       // Subclass-specific attributes and methods
   }
   ```
3. **Access to Superclass Members:** In a subclass, you can access the members (fields and methods) of the superclass using the `super` keyword. This is useful when you want to refer to the superclass's members that are overridden in the subclass.
4. **Method Overriding:** Inheritance often involves overriding methods from the superclass in the subclass. The `@Override` annotation is used to indicate that a method in the subclass is intended to override a method with the same signature in the superclass.
5. **Inheritance Hierarchy:** In Java, you can create multi-level inheritance hierarchies, where a subclass becomes a superclass for another subclass. This allows for creating complex class structures.
6. **Access Modifiers:** In Java, you have control over the visibility of members (fields and methods) of the superclass in the subclass. Access modifiers like `public`, `private`, `protected`, and package-private influence the visibility and accessibility of members.
7. **Object Class:** Every class in Java implicitly or explicitly extends the `Object` class, which is the root class for all Java classes. It provides common methods like `toString`, `equals`, and `hashCode`.

### Has-A relationship or Association
- Has-a relationship is classified into two different things
- The difference between is-a and has-a is that when we have has-a relationship we only use thos property that we want to use
- But when we have is-a relationship all properties by default get inherited from the parent class
    1. Composition 
    2. Aggregation
- Composition or weak relationship when the container object existance does not have any effect on the contained object existance is called as composition
- Aggregatio or strong relationship when the container object existance does effect the contained object existance is called as aggregation 