# 🚀 Constructor Order Trap

## 💻 The Code Execution

So look, I have simply defined a class here named **Parent**. It has its own constructor here. Similarly, there is a **Child** class here which is extending that **Parent** class. And **Child** has its own constructor. Then here I have defined a simple **Test** class, where there is a **main** method. And in the **main** method, I have created an object of the **Child** class.

Here is the setup:

```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}

class Child extends Parent {
    Child() {
        System.out.println("Child Constructor");
    }
}

public class Test {
    public static void main(String[] args) {
        Child ch = new Child();
    }
}

```

So, as soon as you create the object, it is obvious the **Child**'s constructor will be called. We have created the **Child**'s constructor here. So let's see what our output will be.
> **Output:**
> Parent Constructor
> Child Constructor

First, the **Parent** constructor got printed. After that, the **Child** constructor got printed. So why is this happening?

Whenever you create an object of a **Child**, when the **Child**'s constructor is being called here, do you know what the compiler does? Before calling its constructor, it keeps the **Parent**'s object ready. So what it does is, deep down here, it calls the **Parent**'s constructor right now. So here, it actually adds **super**.

**`super():`**

What will happen with this **super**? The parent of this child, its constructor will be called.

> "So if you don't even write `super` from here, by default Java writes it here for you."

So even if I don't write it here, it will work. Even if I write it, it will work.

Here is the explicit addition of `super()`:

```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}

class Child extends Parent {
    Child() {
        super();
        System.out.println("Child Constructor");
    }
}

public class Test {
    public static void main(String[] args) {
        Child ch = new Child();
    }
}

```
> **Output:**
> Parent Constructor
> Child Constructor

Look, first **Parent** got printed, then **Child** got printed.

---

## 🧠 Understanding the Background Mechanism

So let's understand in the background why this is so? Why is this being done? So look, let's try to understand. We had just taken this example, right. There was class **Parent**. It would have some of its own variables. It would have some of its own methods. Similarly, there was class **Child**. It is inheriting its **Parent**. It will also have some of its own variables and methods.

And since it inherits its **Parent**, the things that are in the **Parent** will be accessible in the **Child** as well. So look inside the **Child** class, look, I have also written the **Parent**'s variables and methods. Because since **Child** is extending this **Parent** class, whatever things belong to the **Parent** will be accessible to this **Child** class.

---

## 🏗️ Memory & Inheritance Logic

Here is how the structure maps out:

```text
class Parent {
    // variables <--
    // methods   <--
    x
}

class Child extends Parent {
    // Parent vars/methods
    // child vars/methods
}

```

**Memory Block Representation:**

```text
          Obj (child)
+---------------------------------------+
|  ===> Parent  [✔️]                    |
|  - - - - - - - - - - - - - - - - - -  |
|       child                           |
|  - - - - - - - - - - - - - - - - - -  |
+---------------------------------------+

Child obj = new Child();

```

So whenever you create an object of this **Child** using this, what happens is that when the object is created, let's say you created a **Child**'s object `obj`, right, the **Child**'s object that you created, I just told you that the **Child** has a part of the **Parent** in it and also its own part here, right.

So whenever a **Child**'s object is created, it contains the **Parent**'s entities and also the **Child**'s entities. So look what this means: it is necessary for the **Parent** to also be ready. If the **Parent** is not even created, it is an obvious thing that this will be an overall incomplete object. So the creation of the **Parent** is necessary.

> "That is why the compiler ensures that whenever I create a Child, before the Child, the Parent must be created."

Right? Because the **Child** has extended it. Because if let's say the **Child** is using something of the **Parent** here. Let's say there was a variable named `x` in the **Parent** and it hasn't even initialized, and the **Child** used it here, then before the **Parent** is created, things will go wrong, right. That is why we will always ensure that the **Parent** is created first so that when the **Child** is created, the **Child** can use the **Parent**'s things.

---

## 🏁 Conclusion

That's why the **Parent** must always be ready. After that, then the **Child** is created.

**Execution Flow:**

```text
( Parent is Ready )
        |
        v
( Then child starts )

```
So that's why the order will always be such that the **Parent** will be created first. That is why the **Parent**'s constructor was called first. After that, the **Child** will be created. That is why after that the **Child**'s constructor was called.

And how is this ensured? That in the **Child**'s constructor, first of all, add this one line `super`. If you don't do it, Java will automatically add it for you. What does `super` do? It calls the **Parent**'s constructor.
