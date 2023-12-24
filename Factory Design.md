## Factorty Design 
### Problem Statemetn
- We are creating a bank account making model 
- The bank has to accounts
    - Saving
    - Business
- Depending on what the user wants the corresponding account object is created 
- The sample code looks like this is caled as ``simple factory design`` : 
``
    class account{

        if(some condition is true){
            create business account
        }
        if(some condition is true){
            create 
        }
    }

``
### Problem with the above code
- It is not easily extensible 
- Suppose if we add a new account which is checking 
- Then we need to change present in the account class again  there by it is failing the open close principle 

### Solution
- Have a method which can be overriden by the implementing classes and the corresponding implementing class will give the implementation there by following open close principle will be folowed easily 
- Have a  different class  for creating objects
- Make the class as an interface and let the implementing class create the object 
- This procewss where the eimplementing or the subclass makes the object is called as Factory Method Pattern
- It is called as method because we are overriding a method by the  implementing class which then creates the object

Code
```
// Abstract Product: Furniture Item
interface FurnitureItem {
    void display();
}

// Concrete Products: Sofa, Chair, Table
class Sofa implements FurnitureItem {
    @Override
    public void display() {
        System.out.println("Sofa");
    }
}

class Chair implements FurnitureItem {
    @Override
    public void display() {
        System.out.println("Chair");
    }
}

class Table implements FurnitureItem {
    @Override
    public void display() {
        System.out.println("Table");
    }
}

// Abstract Creator: Furniture Factory
interface FurnitureFactory {
    FurnitureItem createFurniture();
}

// Concrete Creators: Sofa Factory, Chair Factory, Table Factory
class SofaFactory implements FurnitureFactory {
    @Override
    public FurnitureItem createFurniture() {
        return new Sofa();
    }
}

class ChairFactory implements FurnitureFactory {
    @Override
    public FurnitureItem createFurniture() {
        return new Chair();
    }
}

class TableFactory implements FurnitureFactory {
    @Override
    public FurnitureItem createFurniture() {
        return new Table();
    }
}

public class furniture {
    public static void main(String[] args) {
        // Create factories for different types of furniture
        FurnitureFactory sofaFactory = new SofaFactory();
        FurnitureFactory chairFactory = new ChairFactory();
        FurnitureFactory tableFactory = new TableFactory();

        // Create furniture objects using the factory methods
        FurnitureItem sofa = sofaFactory.createFurniture();
        FurnitureItem chair = chairFactory.createFurniture();
        FurnitureItem table = tableFactory.createFurniture();

        // Display the created furniture items
        sofa.display();
        chair.display();
        table.display();
    }
}
```