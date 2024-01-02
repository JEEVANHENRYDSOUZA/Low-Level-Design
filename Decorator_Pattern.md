## Decorator Pattern
### Problem 
- Suppose we are making a notification System 
- The notification class has methods such as establish connectivity to database
- Also the notification class has a method to display the type of notification method being used
- We have different ways of sending a notification 
    1. Whatsapp
    2. Facebook
    3. Email
- These are all independent classes overriding the notification 
- All of these need access to the database which is in the notification class
- Hence the notification type class is extending the notification class
- Depending on which way the client or the user wants the notfication corresponding notification method class object will be created
- But what if the user wants to recieve it via both facebook and email
- So we will have to create another notification method called as facbook_email which will again extend the notification clas
- Here lies the problem 
- What if the number of ways a user receives the notification keeps on increasing
- Hence so will the number of subclasses extending the parent class will also increase
- This leads to a famous problem called as class explosion 
- Class explosion occurs when managing base class becomes very difficult
### Solution 
- The wrapping action in the Decorator Pattern refers to the process of creating an instance of a decorator class and associating it with a component (either a ConcreteComponent or another decorator). This association is typically established through the constructor of the decorator class, where the component to be decorated is passed as an argument.

Here's a step-by-step explanation of the wrapping action:

1. **Create a ConcreteComponent:**
   - First, you create an instance of the ConcreteComponent (e.g., `SimpleCoffee`).

    ```java
    Coffee simpleCoffee = new SimpleCoffee();
    ```

2. **Wrap with Decorators:**
   - You then create instances of decorator classes (e.g., `Milk` and `Sugar`) and pass the `simpleCoffee` instance to their constructors. This is where the wrapping occurs.

    ```java
    Coffee coffeeWithMilk = new Milk(simpleCoffee);
    Coffee coffeeWithMilkAndSugar = new Sugar(coffeeWithMilk);
    ```

   - In these lines, the `Milk` decorator is wrapping the `simpleCoffee` instance, and the `Sugar` decorator is wrapping the `coffeeWithMilk` instance. Each decorator maintains a reference to the component it wraps.

3. **Usage:**
   - You can use the wrapped components (`coffeeWithMilk` and `coffeeWithMilkAndSugar`) just like any other `Coffee` object. The decorators add or modify behavior without altering the structure of the original component.

    ```java
    System.out.println(coffeeWithMilk.getDescription());  // Output: Simple Coffee, with Milk
    System.out.println("Cost: $" + coffeeWithMilk.cost());  // Output: Cost: $3.0

    System.out.println(coffeeWithMilkAndSugar.getDescription());  // Output: Simple Coffee, with Milk, with Sugar
    System.out.println("Cost: $" + coffeeWithMilkAndSugar.cost());  // Output: Cost: $3.5
    ```

- The wrapping action is a dynamic process where decorators are layered upon each other, and each decorator contributes additional behavior to the wrapped component. 
- The decorators form a chain, and the resulting object can be used seamlessly as if it were an instance of the base component interface. This dynamic composition of behavior is a key feature of the Decorator Pattern.

### What if we try static wrapping 
- We will have strong coupling but we always want weak / loose coupling
- In compile-time wrapping, the component and the class doing the wrapping are strongly coupled. 
- This strong coupling is a result of the fact that the composition of the objects is determined at compile time, and any changes to the composition would require modifications to the code.
- When you have a class that directly includes or composes another class at compile time, any modifications to the composition (e.g., adding, removing, or changing components) would require changes to the code of the wrapping class. This direct dependency creates strong coupling between the wrapping class and the components it wraps.

```java
// Component interface
interface Coffee {
    String getDescription();
    double cost();
}

// ConcreteComponent
class SimpleCoffee implements Coffee {
    @Override
    public String getDescription() {
        return "Simple Coffee";
    }

    @Override
    public double cost() {
        return 2.0;
    }
}

// Compile-time wrapping (static composition)
class CoffeeWithMilkAndSugar implements Coffee {
    private SimpleCoffee baseCoffee; // Strong coupling

    public CoffeeWithMilkAndSugar(SimpleCoffee baseCoffee) {
        this.baseCoffee = baseCoffee;
    }

    @Override
    public String getDescription() {
        return baseCoffee.getDescription() + ", with Milk, with Sugar";
    }

    @Override
    public double cost() {
        return baseCoffee.cost() + 1.0 + 0.5;
    }
}
```

- In this example, `CoffeeWithMilkAndSugar` is strongly coupled to `SimpleCoffee` because it directly references and composes an instance of `SimpleCoffee`. 
- Any changes to the component or the composition would require modifications to the `CoffeeWithMilkAndSugar` class.
- It's important to consider the trade-offs between strong coupling and flexibility when choosing a design approach. 
- The classic Decorator Pattern with runtime wrapping provides more flexibility and adheres better to principles like the Open/Closed Principle, allowing for extension without modifying existing code.