## Solid Principles
1. Single Responsibility Principle:
- The Single Responsibility Principle (SRP) states that a class should have only one reason to change, or in other words, it should have only one responsibility. 
- This principle encourages you to keep your classes focused and specialized. Here's an example to illustrate the SRP:
- Suppose you're building a system for managing employees in a company, and you have an `Employee` class. 
- Without adhering to the SRP, you might have a class like this:

```java
public class Employee {
    private String name;
    private int id;

    public void saveEmployee() {
        // Code to save the employee to a database
    }

    public void calculateSalary() {
        // Code to calculate the employee's salary
    }

    public void printEmployeeReport() {
        // Code to print the employee's report
    }
}
```
- In this example, the `Employee` class violates the SRP because it has multiple responsibilities. It's responsible for saving the employee to a database, calculating the employee's salary, and printing employee reports. If any of these responsibilities change or need modifications, you have to touch the same class.
- To adhere to the SRP, you should refactor the class into separate classes, each with a single responsibility
```java
public class Employee {
    private String name;
    private int id;

    // Employee-related properties and methods
}
public class EmployeeSaver {
    public void saveEmployee(Employee employee) {
        // Code to save the employee to a database
    }
}
public class SalaryCalculator {
    public void calculateSalary(Employee employee) {
        // Code to calculate the employee's salary
    }
}

public class ReportPrinter {
    public void printEmployeeReport(Employee employee) {
        // Code to print the employee's report
    }
}
```

2. Open Close Principle
- The Open/Closed Principle (OCP) does indeed state that software entities (classes, modules, functions, etc.) should be open for extension but closed for modification. In other words, you should be able to extend the behavior of a class without changing its source code.
- Let's say you're developing a drawing application, and you have a `Shape` class hierarchy with various shapes, such as `Circle`, `Rectangle`, and `Triangle`. Each shape has a method for calculating its area.

```java
abstract class Shape {
    abstract double calculateArea();
}

class Circle extends Shape {
    private double radius;

    public Circle(double radius) {
        this.radius = radius;
    }

    @Override
    double calculateArea() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    double calculateArea() {
        return width * height;
    }
}

class Triangle extends Shape {
    private double base;
    private double height;

    public Triangle(double base, double height) {
        this.base = base;
        this.height = height;
    }

    @Override
    double calculateArea() {
        return 0.5 * base * height;
    }
}
```

- Now, you want to add a new shape, a `Square`, without modifying the existing code to adhere to the OCP. You can create the `Square` class without changing any of the existing code:

```java
class Square extends Shape {
    private double side;

    public Square(double side) {
        this.side = side;
    }

    @Override
    double calculateArea() {
        return side * side;
    }
}
```


3. Liskov Substituion Principle
- Dervied class must be usable through the base interface , without the need for the user to know the difference 
Certainly, here's a more concrete example of the Liskov Substitution Principle (LSP) using a geometric shapes hierarchy:
- Suppose you have a class hierarchy for geometric shapes: `Shape` is the base class, and `Rectangle` and `Square` are derived classes.

```java
class Shape {
    // Common shape properties and methods
    public double area() {
        return 0;
    }
}

class Rectangle extends Shape {
    private double width;
    private double height;

    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    @Override
    public double area() {
        return width * height;
    }
}

class Square extends Shape {
    private double side;

    public Square(double side) {
        this.side = side;
    }

    @Override
    public double area() {
        return side * side;
    }
}
```
- Now, let's create a function that uses the Liskov Substitution Principle. This function takes a `Shape` object and calculates its area without needing to know the specific derived class.

```java
public class AreaCalculator {
    public double calculateArea(Shape shape) {
        return shape.area();
    }
}
```
- With this design, you can replace instances of the base class (`Shape`) with instances of the derived classes (`Rectangle` and `Square`) without altering the correctness of the program:
```java
Shape shape1 = new Rectangle(5.0, 4.0);
Shape shape2 = new Square(3.0);

AreaCalculator calculator = new AreaCalculator();

System.out.println(calculator.calculateArea(shape1)); // Outputs the rectangle's area
System.out.println(calculator.calculateArea(shape2)); // Outputs the square's area
```
4. Interface Seggration Principle
- The Interface Segregation Principle (ISP) states that clients should not be forced to depend on interfaces they do not use. In other words, an interface should be specific to the needs of the clients that use it, rather than being overly large and imposing unnecessary methods on its clients.
- Here's an example to illustrate the ISP:
- Suppose you are designing software for a document management system. You have different types of documents, and each document can be printed, edited, and shared. You define a generic `Document` interface that includes methods for these actions:

```java
public interface Document {
    void print();
    void edit();
    void share();
}
```
- However, as your system evolves, you introduce different types of documents, such as `TextDocument` and `SpreadsheetDocument`. While it makes sense for a text document to have methods for printing, editing, and sharing, a spreadsheet document might not need the editing feature since it's read-only.
- With the ISP in mind, you should refactor the interface into smaller, more specific interfaces that cater to the needs of each document type. For example:

```java
public interface Printable {
    void print();
}

public interface Editable {
    void edit();
}

public interface Shareable {
    void share();
}

public class TextDocument implements Printable, Editable, Shareable {
    // Text document-specific implementation
}

public class SpreadsheetDocument implements Printable, Shareable {
    // Spreadsheet document-specific implementation
}
```

5. Dependency Inversion Principle
- In object-oriented design, the dependency inversion principle is a specific methodology for loosely coupled software modules. When following this principle, the conventional dependency relationships established from high-level, policy-setting modules to low-level, dependency modules are reversed, thus rendering high-level modules independent of the low-level module implementation details. 
- High-level modules should not import anything from low-level modules. Both should depend on abstractions (e.g., interfaces).
Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.
By dictating that both high-level and low-level objects must depend on the same abstraction, this design principle inverts the way some people may think about object-oriented programming.
- The idea behind points A and B of this principle is that when designing the interaction between a high-level module and a low-level one, the interaction should be thought of as an abstract interaction between them. This not only has implications on the design of the high-level module, but also on the low-level one: the low-level one should be designed with the interaction in mind and it may be necessary to change its usage interface.
- In many cases, thinking about the interaction in itself as an abstract concept allows the coupling of the components to be reduced without introducing additional coding patterns, allowing only a lighter and less implementation-dependent interaction schema.
- When the discovered abstract interaction schema(s) between two modules is/are generic and generalization makes sense, this design principle also leads to the following dependency inversion coding pattern.