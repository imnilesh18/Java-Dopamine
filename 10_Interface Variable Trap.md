# 🚀 Interface Variable Trap

---

## 💻 The Code

So look, what have I done here? I have defined a simple interface, `interface test`, and kept a variable here **x = 10**. And since this is an interface, you can access the variable inside it directly by the interface's name. So, I am trying to modify it. After that, I am looking by printing it to see what its value comes out to be.

```java
interface test {
    int x = 10;
}

class Main {
    public static void main(String[] args) {
        test.x = 20;

        System.out.println(test.x);
    }
}

```

So pause and think about what the output will be. Ideally, it might be coming to your mind that this is **int x = 10**. You modified it. The answer should be 20. But I will run this and see.

---

## ⚠️ The Output & Explanation

It is a compilation error. Look at what this is:

```text
ERROR!
Main.java:7: error: cannot assign a value to static final variable x
        test.x = 20;
               ^

1 error
=== Code Exited With Errors ===

```

> "cannot assign a value to static final variable x"

Now what is the reason for this? Whenever you define a variable inside any interface, by default Java treats it as a **static final** variable. Now what does **final** mean? That it cannot be changed. So a compilation error came right here that you are trying to change a static final variable. Okay? That is why a compilation error came here.

---

## 🔍 Deep Dive: Behind the Scenes

So let's see what is happening here. As soon as we defined a variable inside an interface, Java by default starts treating it like **public static final**. Okay.

```java
// What you write:
interface test {
    int x = 10;
}

// ⬇️ What Java actually interprets it as ⬇️

interface test {
    public static final int x = 10;
}

```

You already know the meaning of **static**, that if something is defined as static, it means it cannot belong to any object. It is a variable of the entire class or interface. Right? This variable cannot belong to any object. It is a variable of the entire interface itself.

And what does **final** mean? That it can no longer be changed.

```java
// Because it is implicitly final:
test.x = 20; // ❌ COMPILATION ERROR

```

That is why as soon as you try to change it, you get a compilation error.