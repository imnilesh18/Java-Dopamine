# 🚀 Static Block Trap

## 🧠 The Scenario

We have a simple `Main` class. It contains a standard `main` method and a `static` block. The question is: **Which one prints first?**

Do not assume the `main` method always executes first. Let's look at the code.

## 💻 The Code

```java
public class Main {

    static {
        System.out.println("Static block");
    }

    public static void main(String[] args) {

        System.out.println("Main block");
    }
}

```

### 🏃‍♂️ output

When we run this code, the output is:

1. `Static block`
2. `Main block`

---

## ⚙️ How It Works (Behind the Scenes)

Why did this happen? People often say "Main executes first," but clearly, that isn't the case here. To understand this, we need to visualize what happens in the background during **Compile Time** vs. **Run Time**.

### 📊 The Execution Flow Diagram

*Based on the internal Java lifecycle:*

| **Compile Time** (`javac`) | **Run Time** (`java`) |
| --- | --- |
| **Command:** `javac Main.java` | **Command:** `java Main` |
| ↓ | ↓ |
| **Java Compiler** reads `Main.java` | **JVM Starts** |
| ↓ | ↓ |
| Checks: **Syntax**, method availability, etc. | `Main.class` is **loaded in Memory** |
| ↓ | ↓ |
| Generates Byte Code (Creates `Main.class`) | **Class Initialization** (Static Phase Begins) 🚩 |
|  | ↓ |
| *At this stage:* | **Execute Static Block** |
| • Static block has **not** executed | ↓ |
| • `main()` has **not** run | **JVM calls `main()` method** |
| • Only `.class` file is created |  |

> **Key Takeaway:** The Static Block executes during the **Class Initialization** phase, which happens *immediately* after the class is loaded into memory and *before* the JVM invokes the `main()` method.

---

## 📝 Step-by-Step Explanation

### 1. Compile Time (`javac`)

When we run `javac Main.java`, the Java Compiler triggers.

* It reads the `Main.java` file.
* It performs syntactical checks (syntax, method loading, etc.).
* It generates a **Byte Code** file known as `Main.class`.
* **Note:** During this phase, *nothing runs*. The static block does not execute, and the main method does not run. It is purely file generation.

### 2. Run Time (`java`)

When we run `java Main`, the JVM (Java Virtual Machine) triggers and takes action:

* **Class Loading:** The Class Loader takes the `Main.class` file and loads it into memory.
* **Class Initialization:** As soon as the class is loaded, initialization begins. This is where **Static** related items (Static blocks, Static variables) are executed and stored in memory.
* **Main Method:** Only *after* the static initialization is complete does the JVM finally call the `main()` method.

---

## ⚡ Simplified Summary

Instead of memorizing complex diagrams, remember this flow:

1. **`javac`** ➔ Generates `.class` (Byte Code).
2. **`java`** ➔ Loads Class into Memory.
3. **Run Static** ➔ (Static Blocks/Variables).
4. **Run `main()**` ➔ (The entry point).