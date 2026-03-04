# 🚀 Why super() Must Be First? | Java Dopamine - 15

"Why must `super()` be first?".

---

## 🛠️ The Problem Setup

In the IDE, a simple **Parent** class is created with a defined constructor. A **Child** class is also created that inherits from the **Parent** class using the `extends` keyword.

Inside the **Child** constructor, a print statement for "Child Constructor" is placed first, and then the **Parent** constructor is called using `super()`.

```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}

class Child extends Parent {
    Child() {
        System.out.println("Child Constructor : ");
        super();
    }
}

class Test {
    public static void main(String[] args) {
        Child obj = new Child();
    }
}

```

In the previous 14_Constructor Order Trap, it was established that the **Parent** must be created before the **Child** object is formed. By default, Java calls the **Parent**'s constructor before forming the **Child** object. If the `super` keyword is not explicitly written, Java automatically inserts it.

However, in this scenario, the `super` keyword is manually written but placed after a print statement.

---

## 🛑 The Error

Running this code results in an error. The error strictly states: `call to super must be first statement in constructor`.

> **Key Takeaway:** This means the `super` call can only be made as the very first statement inside the **Child**'s constructor, and it cannot be placed after anything else.

---

## ✅ The Fix

Moving `super()` to the very first line fixes the problem.

```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}

class Child extends Parent {
    Child() {
        super();
        System.out.println("Child Constructor : ");
    }
}

class Main {
    public static void main(String[] args) {
        Child obj = new Child();
    }
}

```

The output then correctly shows the **Parent** constructor being called before the **Child** constructor.

---

## 🧠 Behind the Scenes: The 'Why'

Behind the scenes, when a **Child** object is created (`Child obj = new Child();`), it inherits the **Parent**.

Because it inherits the **Parent**, the created **Child** object (`obj`) must contain both the **Parent**'s entities/parts and the **Child**'s entities/parts.

**Object Memory Visualization:**

```text
+-------------------------+
|       obj (Child)       |
|  +-------------------+  |
|  |   Parent Parts    |  | <-- Inherited Parent variables/methods
|  +-------------------+  |
|  |   Child Parts     |  | <-- Child's own variables/methods
|  +-------------------+  |
+-------------------------+

```

* This structure implies that the **Parent** must be constructed first before the **Child** can be constructed.
* If the `super` keyword is not called inside the **Child** constructor, Java adds it by default at the very beginning.
* Java strictly enforces that the **Parent** must be formed first before doing anything else, including simple print statements.

---

## ⚠️ A Practical Scenario

A simple example illustrates why this strict rule is necessary:

* Assume the **Parent** class has a variable `int x`.
* This variable `x` is initialized to **10** inside the **Parent**'s constructor (`x = 10;`).
* Suppose the `super` call is placed after a print statement in the **Child** constructor.
* If the **Child** constructor attempts to print the **Parent**'s variable `x` *before* `super()` is executed, the variable has not been initialized yet.
* Since the **Parent**'s constructor hasn't been called, accessing `x` would result in a **garbage value**.

To completely prevent such scenarios, Java simply mandates that the `super` keyword must absolutely be the first statement inside a **Child** constructor. If it is not explicitly written, Java will write it for you by default.