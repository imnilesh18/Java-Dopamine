# 🚀 Functional Interface Trap

---

## 💻 The Problem Setup

Look, here I have defined an interface named **`test`**. And I have applied an annotation **`@FunctionalInterface`**. There are two abstract methods here. You must know that inside interfaces, we only write abstract methods. And any class which implements that interface will have to override all the methods present in that interface.

So, I have a class **`testClass`** here. I haven't done much inside the **`main`** method. I created an object of the **`testClass`** and I am trying to call these overridden methods: **`obj.show()`** and **`obj.print()`**. Look at this.

```java
@FunctionalInterface
interface test {
    void show();
    void print();
}

class testClass implements test {
    public void show() {
        System.out.println("Showing");
    }

    public void print() {
        System.out.println("Printing");
    }
}

class Main {
    public static void main(String[] args) {
        testClass obj = new testClass();
        obj.show();
        obj.print();
    }
}

```

---

## 🛑 The Execution and Error

So, what is the expectation? What will happen?

Let's see what the error is. What is it saying here? **`Unexpected @FunctionalInterface annotation. test is not a functional interface`**. It is saying that this interface **`test`** is not a functional interface. **`multiple non-overriding abstract methods found in interface test`**.

Look, what it actually wants to say is, do you know what a functional interface means?

> An interface which can only have exactly one abstract method.

So here, I had created two abstract methods. That is why we will have to remove one from here. So, we remove **`print`** from here.

---

## ✅ The Solution

```java
@FunctionalInterface
interface test {
    void show();
}

class testClass implements test {
    public void show() {
        System.out.println("Showing");
    }
}

class Main {
    public static void main(String[] args) {
        testClass obj = new testClass();
        obj.show();
    }
}

```

---

## 🧠 Behind the Scenes: Annotations

Now let's go into the background a bit and see what actually happens. So look, what actually happens is that the **`@FunctionalInterface`** I have written here using `@`—these are actually called **annotations**. If you write `@` anywhere in Java, they are called annotations.

And annotations are nothing. They are actually just simple **metadata**.  Meaning, it is used to give some information to the compiler. Or let's assume another person will be reading my code. By reading this annotation, they will definitely get some message in their mind.

```text
@FunctionalInterface  ------>  @ -> Annotations
interface test {
    void show();
    void disp();      ------>  Compiler error;
}

| 1 abstract method |
```

Similarly, what message does the functional interface give? It tells the compiler, "Hey, this interface I am going to write or have written will be a functional interface." And what is the definition of a functional interface? Java understands that there should be only one abstract method in it.

So, if I mistakenly wrote a second abstract method here, or if someone else wrote a second abstract method, the compiler will immediately give you an error right then and there. A compilation error will come to you at that exact moment stating, "Hey, there cannot be multiple abstract methods inside a functional interface." There can only be one abstract method inside a functional interface.

Remember, there should be **only one abstract method**.

And yes, there are many such annotations in Java. This functional interface was just one example I showed you. There are others as well. **`@Override`** is there, **`@Deprecated`** is there, etc. There are many.