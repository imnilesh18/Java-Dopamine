# 🥊 Try vs Finally: Return Statement Behavior

## 🧐 The Scenario

Let's look at video number two in this playlist. Today's question is also interesting: **Try vs Finally**.

Let's go to the IDE to look at the problem, and then we will come back to explain it.

## 💻 The Code

Here is a simple class with a `main` method. I will create an object of the `Main` class. I have defined a method named `test`.

Inside `test`, observe the logic:

* There is a **try block** which is directly returning `10`.
* There is a **finally block** which is returning `20`.

```java
public class Main {
    
    public int test() {
        try {
            return 10;
        } finally {
            return 20; // Bad practice to return value in finally block.
        }
    }

    public static void main(String[] args) {
        
        Main obj = new Main();
        
        System.out.println(obj.test());
        
    }
}

```

If you call `obj.test()`, the `test` function is invoked.
**What will be returned from here?**

> **🛑 Pause & Think:** Don't rush. Pause the video, think calmly, and decide what the output will be.

## 🏃‍♂️ Execution & Output

Let's compile and run this.
**The output is `20`.**

You might be thinking:
*"The `try` block runs first. As soon as `return 10` happens, I should exit the method with 10 as the output."*

But that is not the case.

### 🧠 The Reason

The reason is that the **finally block** is always executed.

> **Key Concept:** The `finally` block runs irrespective of whether an exception occurs in the `try`/`catch` block or if there is a return statement. The `finally` block will **always** execute at the very end.

So, here is what happened:

1. The `try` block attempted to return `10`.
2. However, the `finally` block executed at the end.
3. It **overrode** the last return statement.
4. Therefore, it returned `20` in the end, resulting in `20` as the output.

This is why this is considered a **bad practice**. You might be asked this to quickly check your knowledge: *"Why do we not write return statements inside the finally block?"*

## 🎨 Visual Explanation

Let's look at this visually to understand what happened:

1. **Method Call:** Remember our `test` method. When it was called, we first saw the **try block**.
2. **Try Execution:** The try block executed and attempted to `return 10`.
3. **The Rule:** We have always said that the **finally block** always executes at the end.
4. **Override:** Just as `10` was about to be returned, the `finally` block executed. It performed a `return 20`.
* It **overrode the previous return statement**.
* Because no matter what happens, the `finally` block *must* execute.


5. **Exit:** It overwrote `10` with `20`. When we exited the method, we exited carrying the `20`.

That is why `20` appeared in the output.