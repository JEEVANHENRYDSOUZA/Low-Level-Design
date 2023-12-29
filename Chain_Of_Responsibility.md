## Chain Of Responsibility Pattern
### Introduction 
The Chain of Responsibility Pattern is a behavioral design pattern that allows an object to pass a request along a chain of potential handlers. The idea is to decouple senders and receivers of a request and allow more than one object to handle the request. Each handler in the chain decides either to process the request or to pass it along to the next handler in the chain.

### Components of the Chain of Responsibility Pattern:

1. **Handler:**
   - Declares an interface for handling requests.
   - Optionally, defines a method for setting the next handler in the chain.

2. **ConcreteHandler:**
   - Implements the Handler interface.
   - Handles the request or passes it to the next handler in the chain.

3. **Client:**
   - Initiates the request to a handler in the chain.

### Example Scenario:

Consider a scenario where you have a series of processors to handle a purchase request. Each processor is responsible for approving a certain amount. The processors are arranged in a chain, and a purchase request is passed through the chain until it is approved or rejected.

### UML Diagram:

```
          +-----------------+
          |      Handler    |
          +-----------------+
          |handleRequest()  |
          |setNextHandler() |
          +-----------------+
                  /\
                 /  \
                /    \
               /      \
              /        \
 +-----------------+  +-----------------+
 | ConcreteHandler|  | ConcreteHandler|
 +-----------------+  +-----------------+
 |handleRequest()  |  |handleRequest()  |
 +-----------------+  +-----------------+
```

### Code Example :

```
// Define the abstract base class for order handlers.
abstract class OrderHandler {
    protected OrderHandler nextHandler;

    public OrderHandler(OrderHandler nextHandler) {
        this.nextHandler = nextHandler;
    }

    public abstract void processOrder(String order);
}

// Concrete handler for order validation.
class OrderValidationHandler extends OrderHandler {
    public OrderValidationHandler(OrderHandler nextHandler) {
        super(nextHandler);
    }

    @Override
    public void processOrder(String order) {
        System.out.println("Validating order: " + order);
        // Perform order validation logic here

        // If the order is valid, pass it to the next handler
        if (nextHandler != null) {
            nextHandler.processOrder(order);
        }
    }
}

// Concrete handler for payment processing.
class PaymentProcessingHandler extends OrderHandler {
    public PaymentProcessingHandler(OrderHandler nextHandler) {
        super(nextHandler);
    }

    @Override
    public void processOrder(String order) {
        System.out.println("Processing payment for order: " + order);
        // Perform payment processing logic here

        // If payment is successful, pass it to the next handler
        if (nextHandler != null) {
            nextHandler.processOrder(order);
        }
    }
}

// Concrete handler for order preparation.
class OrderPreparationHandler extends OrderHandler {
    public OrderPreparationHandler(OrderHandler nextHandler) {
        super(nextHandler);
    }

    @Override
    public void processOrder(String order) {
        System.out.println("Preparing order: " + order);
        // Perform order preparation logic here

        // If preparation is complete, pass it to the next handler
        if (nextHandler != null) {
            nextHandler.processOrder(order);
        }
    }
}

// Concrete handler for delivery assignment.
class DeliveryAssignmentHandler extends OrderHandler {
    public DeliveryAssignmentHandler(OrderHandler nextHandler) {
        super(nextHandler);
    }

    @Override
    public void processOrder(String order) {
        System.out.println("Assigning delivery for order: " + order);
        // Perform delivery assignment logic here

        // If delivery is assigned, pass it to the next handler
        if (nextHandler != null) {
            nextHandler.processOrder(order);
        }
    }
}

// Concrete handler for order tracking.
class OrderTrackingHandler extends OrderHandler {
    public OrderTrackingHandler(OrderHandler nextHandler) {
        super(nextHandler);
    }

    @Override
    public void processOrder(String order) {
        System.out.println("Tracking order: " + order);
        // Perform order tracking logic here
    }
}

public class SwiggyOrder {
    public static void main(String[] args) {
        // Create a chain of responsibility for order processing
        OrderHandler orderProcessingChain = new OrderValidationHandler(
            new PaymentProcessingHandler(
                new OrderPreparationHandler(
                    new DeliveryAssignmentHandler(
                        new OrderTrackingHandler(null))))); 
                        // The last handler has no next handler

        // Simulate an order being placed
        String order = "Pizza";
        orderProcessingChain.processOrder(order);
    }
}
```

