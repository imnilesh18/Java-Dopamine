# ☕ Method Overloading vs. Null

## 🧩 The Challenge

Let's look at an interesting problem in Java Method Overloading. We have a `Main` class with a simple setup. inside, we have a method named `testing` that comes in two "flavors" (overloaded versions):

1. `public void testing(Object obj)`
2. `public void testing(String s)`

In the `main` method, we create an instance of the class and call `m.testing(null)`.

**The Question:** When we pass `null`, which method will be called? Will it print from the **Object** method or the **String** method?

```java
public class Main {

    public void testing(Object obj) {
        System.out.println("I am insisde Object method");
    }

    public void testing(String s) {
        System.out.println("I am insisde String method");
    }

    public static void main(String[] args) {
        Main m = new Main();

        m.testing(null);
    }
}

```

Take a moment to pause and guess the answer.

---

## 💡 The Output

When we run this code, the output is:

> **I am insisde String method**

So, the method taking the **String** parameter was actually called. Let's understand why this happened.

---

## 🧠 The Logic: Specificity

The reason is simple if we look at how **Method Overloading** works.

* Method overloading is resolved at **Compile Time**.
* The compiler decides which method to link based on the reference type.
* When multiple methods match, Java picks the one with the **more specific parameter**.

### Class Hierarchy

In Java, `Object` is the parent of the `String` class.

* **Object:** The "Grandparent" of all classes. Every class in Java directly or indirectly inherits from the `Object` class. It is a **generic** concept.
* **String:** This extends `Object`. It is a **child** of Object and represents a **more specific** concept.

The compiler prefers the specific child over the generic parent.

---

## 🚗 The Analogy: Vehicle vs. Car

To visualize this, imagine a hierarchy:

* **Parent (Vehicle):** This is a **generic term**.
* **Child (Car):** This extends Vehicle and is a **specific version** of a vehicle.

When we passed `null` in our code:

* `null` can be assigned to an `Object` (Vehicle).
* `null` can also be assigned to a `String` (Car).

However, just like "Car" is more specific than "Vehicle," **String** is more specific than **Object**. Since the compiler always looks for the most specific match possible, it selects the `String` version of the method.

---

## 🎯 The Golden Rule

Always remember this rule for method overloading:

> **Java selects the method with the more specific parameter type.**