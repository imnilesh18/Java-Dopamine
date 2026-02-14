# ☕ String Comparison: `==` vs `.equals()`

## 📝 The Scenario

Let's dive into the first question of this playlist. Today we are looking at the difference between the double equals operator (`==`) and the `.equals()` method.

Here is the code example directly from the IDE. We are defining two strings using the `new` keyword:

```java
public static void main(String[] args) {
    String s1 = new String("Nilesh");
    String s2 = new String("Nilesh");

    // What will be the output of the following statements?

    System.out.println("s1 == s2: " + (s1 == s2));       // Output: false

    System.out.println("s1.equals(s2): " + s1.equals(s2)); // Output: true
}

```

---

## 🏃‍♂️ The Output

When we compile and run this code, we get the following results:

* `s1 == s2`: **false**
* `s1.equals(s2)`: **true**

Why does this happen? Let's break down the logic.

---

## 🧠 The Concept

### 1. The Double Equals (`==`)

The `==` operator actually checks the **reference** (memory address).

* When we define `s1` using `new String("Nilesh")`, the `new` keyword forces Java to create a **new object** in memory.
* Similarly, for `s2`, we used `new String("Nilesh")`, so another distinct new object is created in memory.

Even though both objects might point to the same underlying string data, `s1` and `s2` are two completely separate objects residing at different memory addresses.

> **Key Takeaway:** Since `s1` and `s2` are different objects, checking their references with `==` results in **false**.

### 2. The `.equals()` Method

The `.equals()` method behaves differently. It actually goes **inside the reference** to check the **value** of the String.

* It looks at the content `s1` is holding ("Nilesh").
* It looks at the content `s2` is holding ("Nilesh").
* Since the string values are identical, the result is **true**.

---

## 🎨 Visualizing Memory & The String Pool

To understand this fully, we need to look at how Java handles memory visually:

1. **The String Pool:** Java maintains a constant space called the **String Pool**. It stores strings here to optimize memory so it doesn't have to recreate the same string repeatedly.
2. **Object Creation (`s1`):** When we execute `s1 = new String("Nilesh")`, Java checks the pool. "Nilesh" is created in the pool. Additionally, because of the `new` keyword, a distinct object `s1` is created in the heap.
3. **Object Creation (`s2`):** When `s2 = new String("Nilesh")` is executed, you are explicitly telling Java you want a **new object**. Java creates the `s2` object.
4. **Optimization:** Java applies logic here. Instead of creating a duplicate "Nilesh" string literal, it makes both the `s1` object and the `s2` object point to the **same** "Nilesh" literal inside the String Pool.

### The Conclusion

* **Physically:** `s1` and `s2` are entirely different objects in the heap with different addresses.
* `s1 == s2` ➔ **False** (Different References).


* **Logically:** Internally, they both point to the same string data ("Nilesh").
* `s1.equals(s2)` ➔ **True** (Same Value).