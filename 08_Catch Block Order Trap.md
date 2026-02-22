# 🚀 Catch Block Order Trap

## 🧠 The Problem

In this scenario, we have a simple `main` method containing a `try` block where we attempt to divide by zero (`int a = 10/0;`), which will obviously throw an exception. We then try to handle this with two catch blocks: first catching `Exception`, and then catching `ArithmeticException`.

Here is what the initial code looks like:

```java
public class Main {
    public static void main(String[] args) {
        try {
            int a = 10/0;
        } catch (Exception e) {
            System.out.println(e.getMessage());
        } catch (ArithmeticException e) {
            System.out.println(e.getMessage());
        }
    }
}

```

If you try to run this code, you will encounter a compilation error:

```text
ERROR!
Main.java:7: error: exception ArithmeticException has already been caught
        } catch (ArithmeticException e) {
          ^
1 error

```

The compiler is explicitly stating that the `ArithmeticException` has already been caught by the preceding `Exception` block. This indirectly tells us that the order in which we wrote our catch blocks is incorrect.

---

## 🔍 Why Does This Happen?

To understand why this happens in the background, we need to look at the hierarchical diagram of exceptions in Java.

> **Key Concept:** `Exception` is a **Parent class**, and `ArithmeticException` is its **Child class**.

If we look at a slightly larger (though still simplified) view of the Java exception hierarchy:

```text
       Object
         |
         v
     Throwable
      /     \
     v       v
   Error   Exception
             |
            ...
             |
             v
    ArithmeticException

```

*Note: The actual hierarchy is much larger, including checked and unchecked exceptions, but this illustrates the core relationship.*

When the compiler reads your code, it sees that you are trying to cover the `Exception` class type first. Because `Exception` is the parent (or "father") of `ArithmeticException`, the `ArithmeticException` is inherently already covered by the first catch block.

Because of this parent-child relationship, if an `ArithmeticException` occurs in the `try` block, it will immediately be caught by the generic `Exception` catch block. Consequently, the execution flow will never reach the second catch block designated specifically for `ArithmeticException`.

> **The Golden Rule:** Java never allows an **unreachable catch block**.

This is why Java throws a compilation error right away, warning you that the code block is unreachable and useless.

---

## 🛠️ The Fix

To fix this issue, you have two options:

1. Remove the `ArithmeticException` block entirely.
2. Place the catch blocks in the correct order.

Always write the most **specific** exception first. `Exception` is a generic term, while `ArithmeticException` is a specifically defined type of exception. Therefore, the specific exception must precede the generic one.

Here is the corrected code:

```java
public class Main {
    public static void main(String[] args) {
        try {
            int a = 10/0;
        } catch (ArithmeticException e) {
            System.out.println(e.getMessage());
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
    }
}

```

By placing `ArithmeticException` first, it gets the chance to catch the specific divide-by-zero error. Any other generic exceptions that occur will bypass it and get caught by the subsequent `Exception` block. Running this corrected code successfully outputs `/ by zero`.