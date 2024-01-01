## State Pattern
### Introucduction
- The State Pattern is a behavioral design pattern that allows an object to alter its behavior when its internal state changes. 
- This pattern is particularly useful in scenarios where an object can exist in different states and its behavior depends on the current state. 
- The State Pattern achieves this by representing each state as a separate class and delegating the state-specific behavior to these classes.

### Participants in the State Pattern:

1. **Context:**
   - Maintains an instance of the current state and delegates state-specific behavior to the state objects.
   - The context class represents the object whose behavior varies based on its internal state.

2. **State:**
   - Defines an interface or abstract class for encapsulating the behavior associated with a particular state.
   - Concrete state classes implement this interface or extend the abstract class, providing the specific behavior for each state.

#### Example in Java:

Let's consider an example of a `TrafficLight` system, where the traffic light can be in different states: `Red`, `Yellow`, and `Green`. Each state will have its own behavior.

```java
// State interface
interface TrafficLightState {
    void handleRequest();
}

// Concrete state classes
class RedState implements TrafficLightState {
    @Override
    public void handleRequest() {
        System.out.println("Switching to Green");
    }
}

class YellowState implements TrafficLightState {
    @Override
    public void handleRequest() {
        System.out.println("Switching to Red");
    }
}

class GreenState implements TrafficLightState {
    @Override
    public void handleRequest() {
        System.out.println("Switching to Yellow");
    }
}

// Context class
class TrafficLight {
    private TrafficLightState currentState;

    public TrafficLight() {
        // Initial state is Red
        currentState = new RedState();
    }

    public void requestStateChange() {
        currentState.handleRequest();
        // Transition to the next state
        if (currentState instanceof RedState) {
            currentState = new GreenState();
        } else if (currentState instanceof GreenState) {
            currentState = new YellowState();
        } else if (currentState instanceof YellowState) {
            currentState = new RedState();
        }
    }
}

// Client code
public class StatePatternExample {
    public static void main(String[] args) {
        TrafficLight trafficLight = new TrafficLight();

        // Simulating state changes
        trafficLight.requestStateChange();  // Red to Green
        trafficLight.requestStateChange();  // Green to Yellow
        trafficLight.requestStateChange();  // Yellow to Red
    }
}
```
- The above code has tight counpling to further make it lossely coupled to further reduce coup;ing we can refactor the code as


```java
// Updated State interface
interface TrafficLightState {
    void handleRequest(TrafficLight context);
}

// Updated Concrete state classes
class RedState implements TrafficLightState {
    @Override
    public void handleRequest(TrafficLight context) {
        System.out.println("Switching to Green");
        context.setState(new GreenState());
    }
}

class YellowState implements TrafficLightState {
    @Override
    public void handleRequest(TrafficLight context) {
        System.out.println("Switching to Red");
        context.setState(new RedState());
    }
}

class GreenState implements TrafficLightState {
    @Override
    public void handleRequest(TrafficLight context) {
        System.out.println("Switching to Yellow");
        context.setState(new YellowState());
    }
}

// Updated Context class
class TrafficLight {
    private TrafficLightState currentState;

    public TrafficLight() {
        // Initial state is Red
        currentState = new RedState();
    }

    public void requestStateChange() {
        currentState.handleRequest(this);
    }

    public void setState(TrafficLightState newState) {
        currentState = newState;
    }
}

// Client code
public class StatePatternExample {
    public static void main(String[] args) {
        TrafficLight trafficLight = new TrafficLight();

        // Simulating state changes
        trafficLight.requestStateChange();  // Red to Green
        trafficLight.requestStateChange();  // Green to Yellow
        trafficLight.requestStateChange();  // Yellow to Red
    }
}
```

