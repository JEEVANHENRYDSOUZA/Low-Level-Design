## Observer Pattern 
### Problem 
- Suppose we are designing a weather app for different users
- As soon as the weeather changes all users must be notified immediately of the change 
- Once they are notified about the change the corresponding weather values should also change
- There are two ways to acheive this behavior
    1. The users keep on sending requests to a user at a given interval of time and 
    keep on asking the weather app is there any changes
    2. This method is called as polling
    3. Drawback of using polling is what if the changes occur within the interval of time
    4. Then the users wont be notified
    5. Hence we do not use this approach , instead we want the weather app to notify all the users that there is a change 

### Main Goal 
- Hence the main goal of  observer pattern is to change from polling to push functionality
### Observer Pattern
-  We have teo interfaces here 
    1. Observer : the interface waiting or looking for state change
    2. Observerable: the interface that is undergoing a state change 
- Also there are multiple variations of the observer pattern available
- We are looking in toe the variation where we do not pass the refernce of the observer to the observable
### Code
```
import java.util.*;

interface Observer {
    void update(Order order);
}

class Customer implements Observer {
    private String name;

    public Customer(String name) {
        this.name = name;
    }

    @Override
    public void update(Order order) {
        System.out.println("Hello, " + name + "! Order #" + order.getId() + " is now " + order.getStatus() + ".");
    }
}

class Restaurant implements Observer {
    private String restaurantName;

    public Restaurant(String name) {
        this.restaurantName = name;
    }

    @Override
    public void update(Order order) {
        System.out.println("Restaurant " + restaurantName + ": Order #" + order.getId() + " is now " + order.getStatus() + ".");
    }
}

class DeliveryDriver implements Observer {
    private String driverName;

    public DeliveryDriver(String name) {
        this.driverName = name;
    }

    @Override
    public void update(Order order) {
        System.out.println("Driver " + driverName + ": Order #" + order.getId() + " is now " + order.getStatus() + ".");
    }
}

class CallCenter implements Observer {
    @Override
    public void update(Order order) {
        System.out.println("Call center: Order #" + order.getId() + " is now " + order.getStatus() + ".");
    }
}

class Order {
    private int id;
    private String status;
    private List<Observer> observers = new ArrayList<>();

    public Order(int id) {
        this.id = id;
        this.status = "Order Placed";
    }

    public int getId() {
        return id;
    }

    public String getStatus() {
        return status;
    }

    public void setStatus(String newStatus) {
        status = newStatus;
        notifyObservers();
    }

    public void attach(Observer observer) {
        observers.add(observer);
    }

    public void detach(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(this);
        }
    }
}

public class OrderStatus {
    public static void main(String[] args) {
        // Create an order
        Order order1 = new Order(123);

        // Create customers, restaurants, drivers, and a call center to track the order
        Customer customer1 = new Customer("Customer 1");
        Restaurant restaurant1 = new Restaurant("Rest 1");
        DeliveryDriver driver1 = new DeliveryDriver("Driver 1");
        CallCenter callCenter = new CallCenter();

        // Attach observers to the order
        order1.attach(customer1);
        order1.attach(restaurant1);
        order1.attach(driver1);
        order1.attach(callCenter);

        // Simulate order status updates
        order1.setStatus("Out for Delivery");

        // Detach an observer (if needed)
        order1.detach(callCenter);

        // Simulate more order status updates
        order1.setStatus("Delivered");
    }
}

```