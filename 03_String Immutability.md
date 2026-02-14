# 🚀 String Immutability Challenge

Let's look at a tricky question regarding **String Immutability** that is often asked in interviews to test your knowledge of how Java handles Strings internally.

## 🧠 The Puzzle: Guess the Output

Consider the following code snippet. We have a simple `Main` class with a String variable `s`. We perform a concatenation operation and then print `s`.

**Pause here and guess: What will be the output?**

```java
public class Main {
    public static void main(String[] args) {
        String s = "codestorywith";

        s.concat("MIK");

        System.out.println(s);
    }
}

```

---

## 🧐 The Explanation

If you compile and run the code above, the output is:
`codestorywith`

Even though we called `s.concat("MIK")`, the string "MIK" was **not** appended to the original reference `s`.

### Why did this happen?

The reason lies in the nature of String objects in Java:

> **Key Concept:** When you create a String object in Java, it is **constant** (Immutable). Once a String object is created, it cannot be changed.

When you executed `s.concat("MIK")`, Java actually did the following:

1. It created a **new** String object with the value `"codestorywithMIK"`.
2. However, this new object was not assigned to any variable.
3. The variable `s` still points to the original object `"codestorywith"`.

---

## 🛠️ The Fix

To see the modified string, you must either reassign `s` or assign the result of the concatenation to a **new String variable**.

Here is the corrected code:

```java
public class Main {
    public static void main(String[] args) {
        String s = "codestorywith";

        // Assign the result to a new variable (or reassign to s)
        String newS = s.concat("MIK"); // codestorywithMIK

        System.out.println(newS);
    }
}

```

**Output:**
`codestorywithMIK`

---

## 🎨 Visualizing Memory (Heap & String Pool)

Let's look at what is happening under the hood in the Java Memory (Heap).

1. **Initialization:** When we write `String s = "codestorywith";`, a String object is created in the Heap (specifically stored in the **String Pool**) and `s` points to it.
2. **Concatenation:** When `s.concat("MIK")` is executed, Java creates a **new String object** in memory with the value `"codestorywithMIK"`.
3. **References:**
* The original `s` reference **still points** to the old object (`"codestorywith"`).
* The new object (`"codestorywithMIK"`) is created, but initially, nothing points to it (unless we assign it).


4. **Assignment:** By using `String newS = ...`, we create a new reference `newS` that points to this newly created object.