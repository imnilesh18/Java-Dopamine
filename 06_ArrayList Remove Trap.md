# 🚨 ArrayList Remove Trap

## 💻 The Scenario

I have taken a simple `ArrayList` and added three elements to it: `10`, `20`, and `30`.

If I print this list, the output should simply be `[10, 20, 30]`.

```java
public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> al = new ArrayList<Integer>();

        al.add(10);
        al.add(20);
        al.add(30);

        System.out.println(al); 
    }
}

```

Now, pay attention. I am adding a line to remove `10` from the ArrayList. My expectation is that the value `10` gets removed, and when I print the list afterward, only `20` and `30` should be printed.

```java
        // Attempting to remove the value 10
        al.remove(10); 

        System.out.println(al);
    }
}

```

---

## 💥 The Crash

When we run the code above, we encounter an exception:

> **Exception:** `java.lang.IndexOutOfBoundsException: Index 10 out of bounds for length 3`

This error is telling us that in this line, the **index is 10**, while the size of the list is only 3. It is throwing an `OutOfBoundsException`.

This means that `10` is actually working as an **index** here.

---

## ✅ The Solution

If you want to remove an element (the value itself) from an `ArrayList`, you have to specifically tell Java: *"I am not talking about the index here. I want to remove the value `10`."*

To do this, we wrap the value using `Integer.valueOf()`.

```java
        // Correct way to remove the object/value 10
        al.remove(Integer.valueOf(10));

        System.out.println(al);

```

**Output:**

```
[10, 20, 30]
[20, 30]

```

Now it works as expected.

---

## 🧠 Behind the Scenes: Method Overloading

What is actually happening in the background? The `ArrayList` class has **two overloaded flavors** of the `remove()` method:

1. `remove(int index)`
2. `remove(Object o)`

### How Java Decides Which Method to Call:

* **The Trap Case:**
When you call `remove(20)` (or `10` in our example), Java sees that `20` is a normal primitive `int`, not an object. Therefore, it calls the **first** flavor: `remove(int index)`. It assumes you are passing an index.
```text
remove(20);  -------->  Calls: remove(int index)

```


* **The Working Case:**
When you call `Integer.valueOf(20)`, it actually returns an **Integer Object**.
When you pass this Integer Object to the remove function, `ArrayList` decides: *"Okay, an Object is coming in."* Consequently, it calls the **second** flavor: `remove(Object o)`.
```text
Integer o = Integer.valueOf(20);
      |
      v
remove(o);   -------->  Calls: remove(Object o)

```



### 🔑 Key Takeaway

Always be mindful when removing integers from an `ArrayList<Integer>`. If you pass a primitive, it treats it as an **index**. If you pass an object, it treats it as the **element to be removed**.