# 🚀 Static Block vs Constructor
---

## 🧩 The Code Problem

First, there is a class `Test`. Inside it, I have defined a `static int x`. There is a static block, then an instance block section, and finally a constructor.

```java
public class Test {
    static int x = 10;

    static {
        x += 5;
    }

    //instance block
    {
        x = x + 2;
    }

    Test() {
        x = x + 3;
    }

    public static void main(String[] args) {
        Test t1 = new Test();
        Test t2 = new Test();
        System.out.println(x);
    }
}

```

Look here what I did: I created an object named `t1`, another object named `t2`, and I am printing the value of `x`. Pause and think for yourself what the final value of this **x** will be.

---

## 🤔 The Common Misconception

Many of you might be thinking that since it's static, static variables belong to a class and not to every instance. Static is common for all objects because it belongs to the class.

So, the value of **x** is 10. After that, the static block would have been called, so 10 + 5 would have become 15. And the constructor is called twice here because I created the object twice. So 10 + 5 was 15, 15 + 3 = 18, then the second time the constructor would be called, 18 + 3 would become 21.

We don't know when this instance block is called. So we are expecting the answer to be 21. But if I run this, the answer comes out to **25**.

---

## 🧠 The Concept & Step-by-Step Execution

> **The actual reason:** Whenever a class loads, the static parts load right at the beginning. It belongs to the class.

* So 10 and 5, which is 15, both of these would have executed because both are static blocks. So the value of **x** became 15.
* After that, when you created two objects, whenever an object is created, their instance block gets called. Actually, this is called an **instance block**.
* So once when this object `t1` was created, this instance block was called for that object. So the value of **x** was 15 before, now it has become 17.
* And yes, one more thing, when you created the object, its constructor would also have been called. So 17 + 3 became 20.
* After that, similarly, when you created the second object `t2`, its instance block was called first. 20 + 2 became 22 for the value of **x**.
* Then its constructor was called, so 22 + 3 became 25.

So in the end, the output is **25**.

---

## 📊 Visual Execution Order

Let's go visually and see what the actual order is in which these blocks are executed. Remembering this is very simple.

**When the class Loads:**

1. **Static variables and static blocks:** Run once, when class loads.

**When an object is created:**
2.  **Instance blocks:** Run every time an object is created.
3.  **Constructor:** Runs after instance blocks, for each object.

> **Summary Flow:**
> **Class Loads** ➔ Static stuff runs once
> **Object Created** ➔ Instance Blocks ➔ Constructor

So what is the order actually? First, when the class loaded, the static parts ran. And whenever I created an object of that class, first the instance blocks were called for that object, and after that, the constructor was called for that object. This is always the order.

---

## 🛠️ The Proof in Code

If you look at this code as well and run it, look carefully. I have printed "Static Block" in the static block here. Then there is an instance block here, and a constructor here.

```java
class Test {
    static {
        System.out.println("Static Block");
    }

    {
        System.out.println("Instance Block");
    }

    Test() {
        System.out.println("Constructor");
    }
}

```

If I create an object of this class now: `Test obj = new Test();`, look what will happen.

1. First, the class would have loaded. As soon as the class loads, this static block would have already been printed. First, this would have been printed.
2. After that, as soon as I created an object, its instance block would have been printed.
3. Then, I created the object, so its constructor will also be called. As soon as the constructor is called, this statement would have been printed.

So this is the order that you have to remember.