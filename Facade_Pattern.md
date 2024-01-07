## Facade Pattern
### Introduction 
- The meaning of Facade in english is the  outside structure of a building
- The Facade Pattern is a structural design pattern that provides a simplified interface to a set of interfaces in a subsystem, making it easier to use. It involves creating a class, known as the facade, which represents a higher-level interface that makes the subsystem easier to use.

The main purpose of the Facade Pattern is to hide the complexities of a subsystem and provide a simpler interface for the client code. It acts as a wrapper around the existing interfaces of a subsystem to make them more accessible and user-friendly. Clients interact with the facade instead of directly interacting with the individual components of the subsystem.

Key components of the Facade Pattern:

1. **Facade:** This is the main class that clients interact with. It represents a unified interface to the subsystem. The facade delegates client requests to appropriate objects within the subsystem.

2. **Subsystems:** These are the individual classes or components that make up the subsystem. They perform the actual work requested by the client. The facade does not encapsulate these subsystems but rather delegates the work to them.



```java
// Subsystem components
class SubsystemA {
    public void operationA() {
        System.out.println("SubsystemA: Performing operation A");
    }
}

class SubsystemB {
    public void operationB() {
        System.out.println("SubsystemB: Performing operation B");
    }
}

class SubsystemC {
    public void operationC() {
        System.out.println("SubsystemC: Performing operation C");
    }
}

// Facade
class Facade {
    private SubsystemA subsystemA;
    private SubsystemB subsystemB;
    private SubsystemC subsystemC;

    public Facade() {
        this.subsystemA = new SubsystemA();
        this.subsystemB = new SubsystemB();
        this.subsystemC = new SubsystemC();
    }

    public void operationFacade() {
        // Simplified interface that delegates to the subsystems
        subsystemA.operationA();
        subsystemB.operationB();
        subsystemC.operationC();
    }
}

// Client code
public class FacadePatternExample {
    public static void main(String[] args) {
        Facade facade = new Facade();
        facade.operationFacade();
    }
}
```



