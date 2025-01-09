# Generics

### Type Erasure
Generics were introduced to the Java language to provide tighter type checks at compile time and to support generic programming. To implement generics, the Java compiler
applies type erasure to:

• Replace all type parameters in generic types with their bounds or Object if the type parameters are unbounded. The produced bytecode, therefore, contains only ordinary
  classes, interfaces, and methods.
• Insert type casts if necessary to preserve type safety.
• Generate bridge methods to preserve polymorphism in extended generic types.

Type erasure ensures that no new classes are created for parameterized types; consequently, generics incur no runtime overhead.

We need **generics** in Java to improve code **safety, reusability, and readability**. Generics allow us to create classes, methods, and interfaces that can operate on **different types** of data while ensuring **type safety** at compile time. Here’s why generics are essential:

---

### 1. **Type Safety**:
   - Without generics, you might need to use `Object` to handle different types of data, which can lead to **runtime errors** if incorrect types are used.
   - Generics enforce **compile-time type checking**, reducing the risk of `ClassCastException` at runtime.

   **Without Generics (Pre-Java 5)**:
   ```java
   List list = new ArrayList();
   list.add("Hello");
   list.add(42); // Allowed, but can cause issues later
   
   String s = (String) list.get(1); // Runtime error: ClassCastException
   ```

   **With Generics**:
   ```java
   List<String> list = new ArrayList<>();
   list.add("Hello");
   // list.add(42); // Compile-time error: incompatible types

   String s = list.get(0); // No casting needed, and it's safe
   ```

   - Generics ensure that only objects of the specified type (`String` in this case) can be added to the list.

---

### 2. **Elimination of Manual Type Casting**:
   - Without generics, you must manually cast objects retrieved from collections like `List`, `Set`, or `Map`.
   - With generics, the casting is handled automatically, simplifying the code.

   **Without Generics**:
   ```java
   List list = new ArrayList();
   list.add("Hello");
   String s = (String) list.get(0); // Manual casting required
   ```

   **With Generics**:
   ```java
   List<String> list = new ArrayList<>();
   list.add("Hello");
   String s = list.get(0); // No casting needed
   ```

---

### 3. **Code Reusability**:
   - Generics enable the creation of **reusable code components** that work with different data types without duplication.

   **Example: Generic Method**:
   ```java
   public static <T> void printArray(T[] array) {
       for (T element : array) {
           System.out.println(element);
       }
   }

   public static void main(String[] args) {
       Integer[] intArray = {1, 2, 3};
       String[] strArray = {"A", "B", "C"};
       
       printArray(intArray); // Works with Integer
       printArray(strArray); // Works with String
   }
   ```

   - The `printArray` method works for any type (`Integer`, `String`, etc.), making it highly reusable.

---

### 4. **Improved Readability and Maintainability**:
   - Generics make the code more self-explanatory by specifying the types of objects a class or method will work with.
   - Developers can understand the type constraints and purpose of the code more easily.

   **Example**:
   ```java
   Map<String, Integer> studentGrades = new HashMap<>();
   ```
   - From the declaration, it's clear that `studentGrades` maps `String` keys (student names) to `Integer` values (grades).

---

### 5. **Generic Data Structures**:
   - Generics are especially powerful for creating **data structures** that can work with different types of data.

   **Example: Generic Class**:
   ```java
   public class Box<T> {
       private T value;

       public void setValue(T value) {
           this.value = value;
       }

       public T getValue() {
           return value;
       }
   }

   public static void main(String[] args) {
       Box<Integer> intBox = new Box<>();
       intBox.setValue(123);
       System.out.println(intBox.getValue());

       Box<String> strBox = new Box<>();
       strBox.setValue("Hello");
       System.out.println(strBox.getValue());
   }
   ```

   - The `Box` class can hold any type of data (`Integer`, `String`, etc.), making it versatile and reusable.

---

### 6. **Backward Compatibility with Legacy Code**:
   - Generics were introduced in Java 5, and they are designed to be backward-compatible with older code that uses raw types. This ensures a smooth transition for developers using legacy code.

---

### 7. **Use with Collections Framework**:
   - Generics are heavily used in the **Java Collections Framework** to ensure type safety and prevent runtime errors.

   **Example**:
   ```java
   List<String> names = new ArrayList<>();
   names.add("Alice");
   names.add("Bob");
   // names.add(42); // Compile-time error: incompatible types
   ```

---

### Summary of Benefits:
- **Type safety**: Catch type-related errors at compile time.
- **Elimination of casting**: Simplifies code and reduces potential runtime errors.
- **Code reusability**: Enables writing generic, reusable algorithms and data structures.
- **Improved readability**: Makes the purpose and usage of the code more clear.
- **Essential for collections**: Provides type safety when working with collections like `List`, `Set`, and `Map`.

---

### Conclusion:
Generics in Java enhance **type safety, reusability, and readability** of code. They allow you to write flexible and efficient code while reducing the risk of runtime errors, making them an essential feature in modern Java programming.

## Custom ArrayList

```
import java.util.ArrayList;
import java.util.Arrays;

public class CustomArrayList {

    private int[] data;
    private static int DEFAULT_SIZE = 10;
    private int size = 0; // also working as index value

    public CustomArrayList() {
        this.data = new int[DEFAULT_SIZE];
    }

    public void add(int num) {
        if (isFull()) {
            resize();
        }
        data[size++] = num;
    }

    private void resize() {
        int[] temp = new int[data.length * 2];

        // copy the current items in the new array
        for (int i = 0; i < data.length; i++) {
            temp[i] = data[i];
        }
        data = temp;
    }

    private boolean isFull() {
        return size == data.length;
    }

    public int remove() {
        int removed = data[--size];
        return removed;
    }

    public int get(int index) {
        return data[index];
    }

    public int size() {
        return size;
    }

    public void set(int index, int value) {
        data[index] = value;
    }

    @Override
    public String toString() {
        return "CustomArrayList{" +
                "data=" + Arrays.toString(data) +
                ", size=" + size +
                '}';
    }

    public static void main(String[] args) {
//        ArrayList list = new ArrayList();
        CustomArrayList list = new CustomArrayList();
//        list.add(3);
//        list.add(5);
//        list.add(9);

        for (int i = 0; i < 14; i++) {
            list.add(2 * i);
        }

        System.out.println(list);

        ArrayList<Integer> list2 = new ArrayList<>();
//        list2.add("dfghj");
    }
}
```

### Custom Generic ArrayList

```
import java.util.ArrayList;
import java.util.Arrays;

// https://docs.oracle.com/javase/tutorial/java/generics/restrictions.html#createObjects

public class CustomGenArrayList<T> {

    private Object[] data;
    private static int DEFAULT_SIZE = 10;
    private int size = 0; // also working as index value

    public CustomGenArrayList() {
        data = new Object[DEFAULT_SIZE];
    }

    public void add(T num) {
        if (isFull()) {
            resize();
        }
        data[size++] = num;
    }

    private void resize() {
        Object[] temp = new Object[data.length * 2];

        // copy the current items in the new array
        for (int i = 0; i < data.length; i++) {
            temp[i] = data[i];
        }
        data = temp;
    }

    private boolean isFull() {
        return size == data.length;
    }

    public T remove() {
        T removed = (T)(data[--size]);
        return removed;
    }

    public T get(int index) {
        return (T)data[index];
    }

    public int size() {
        return size;
    }

    public void set(int index, T value) {
        data[index] = value;
    }

    @Override
    public String toString() {
        return "CustomGenArrayList{" +
                "data=" + Arrays.toString(data) +
                ", size=" + size +
                '}';
    }

    public static void main(String[] args) {
//        ArrayList list = new ArrayList();
        CustomGenArrayList list = new CustomGenArrayList();
//        list.add(3);
//        list.add(5);
//        list.add(9);

//        for (int i = 0; i < 14; i++) {
//            list.add(2 * i);
//        }

//        System.out.println(list);

        ArrayList<Integer> list2 = new ArrayList<>();
//        list2.add("dfghj");


        CustomGenArrayList<Integer> list3 = new CustomGenArrayList<>();
        for (int i = 0; i < 14; i++) {
            list3.add(2 * i);
        }

        System.out.println(list3);

    }
}
```

### Note: If we want type to be tightly bound, we can make use of wildcard.

```
// https://docs.oracle.com/javase/tutorial/java/generics/restrictions.html#createObjects

// here T should either be Number or its subclasses
public class WildcardExample<T extends Number> {
}

public void getList(List<? extends Number> list) {
  // do something
}
```

