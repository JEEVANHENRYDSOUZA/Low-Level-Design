## Interator Pattern
### Introdudction 
-  In the Iterator Pattern, the idea is to provide a specific iterator for each type of collection. This allows for flexibility and adaptability, as different types of collections may have different structures and therefore different ways of iterating over their elements.

Here's a summary of how this works:

1. **Collection Interface (`Iterable`):**
   - A collection class typically implements the `Iterable` interface. This interface declares the `iterator()` method, which returns an iterator specific to that collection.

2. **Iterator Interface:**
   - The `Iterator` interface declares methods like `hasNext()` and `next()` that define the standard way to traverse the elements. This interface is implemented by specific iterator classes.

3. **Specific Iterator Implementation:**
   - Each collection class provides its specific iterator implementation, usually as a nested or separate class. This iterator knows how to traverse the elements of that particular collection type.

4. **Client Code:**
   - The client code, which wants to iterate over the elements of a specific collection, obtains an iterator from the collection through the `iterator()` method. The client then uses the iterator's methods (`hasNext()` and `next()`) to traverse the elements without knowing the details of the collection's internal structure.

Here's a simple example extending the previous one to illustrate the concept:

```java
import java.util.Iterator;
import java.util.NoSuchElementException;

// Collection interface
public interface Iterable<T> {
    Iterator<T> iterator();
}

// Array collection class
// we will not take care of how these methods are implemented 
public class ArrayCollection<T> implements Iterable<T> {
    private T[] elements;
    private int size;

    public ArrayCollection(T[] elements) {
        this.elements = elements;
        this.size = elements.length;
    }

    // Specific iterator for ArrayCollection
    // we will not take care of how these methods are implemented 
    private class ArrayIterator implements Iterator<T> {
        private int currentIndex = 0;

        @Override
        public boolean hasNext() {
            return currentIndex < size;
        }

        @Override
        public T next() {
            if (!hasNext()) {
                throw new NoSuchElementException();
            }
            return elements[currentIndex++];
        }
       
        @Override
        public void remove() {
            throw new UnsupportedOperationException("Remove operation not supported");
        }
    }

    // Implementation of the Iterable interface
    @Override
    public Iterator<T> iterator() {
        return new ArrayIterator();
    }

    public static void main(String[] args) {
        Integer[] array = {1, 2, 3, 4, 5};
        ArrayCollection<Integer> collection = new ArrayCollection<>(array);

        // Using enhanced for loop
        for (Integer element : collection) {
            System.out.println(element);
        }
    }
}
```

