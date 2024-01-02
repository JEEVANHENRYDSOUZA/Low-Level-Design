## Adapter Pattern
### Introduction
- We are not changing the behavior but just want the interface to be compatble
- By compatible I mean using the interface  method signature of a particular constructor to call a method having a different signature 
- Compatibility in the Adapter Pattern is achieved using constructor injection. The Adapter Pattern involves creating a class (the adapter) that bridges the gap between two incompatible interfaces. 
- Constructor injection is one way to pass the necessary dependencies into the adapter.

Here's a breakdown of how constructor injection is typically used in the Adapter Pattern:

1. **Target Interface:**
   - This is the interface that the client code expects or relies on.

2. **Adaptee Class:**
   - This is the existing class with a different interface that needs to be adapted.

3. **Adapter Class:**
   - The adapter class implements the target interface and holds an instance of the adaptee class. It acts as a wrapper, translating calls from the target interface to the adaptee's interface.

4. **Constructor Injection:**
   - The adapter class receives an instance of the adaptee class through its constructor. This is where the constructor injection occurs.

Here's a simple example to illustrate the concept:

```java
// Target interface
interface Target {
    void request();
}

// Adaptee (existing class with a different interface)
class Adaptee {
    void specificRequest() {
        System.out.println("Adaptee's specific request");
    }
}

// Adapter
class Adapter implements Target {
    private Adaptee adaptee;

    // Constructor injection
    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    @Override
    public void request() {
        // Using the existing Adaptee's functionality in a way that conforms to the Target interface
        adaptee.specificRequest();
    }
}

// Client code
public class AdapterPatternExample {
    public static void main(String[] args) {
        // Using an existing Adaptee class through the Adapter with constructor injection
        Adaptee adaptee = new Adaptee();
        Target adapter = new Adapter(adaptee);

        // The client interacts with the Target interface
        adapter.request();
    }
}
```

