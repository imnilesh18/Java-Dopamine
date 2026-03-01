# 🚀 The Default Method Trap in Java Interfaces
---

## 🛠️ The Initial Setup

Look, I have defined a simple interface here named **`test`**. It has an abstract method **`show`**, and the class **`testClass`** is implementing this **`test`** interface. Obviously, since it is an abstract method, it has to implement it. So, it has implemented it here.

And here in the **`Main`** method, I created a **`testClass`** object and we are calling **`obj.show()`**. So this will run. Let's assume in the future you get a requirement that you have to add one more method here, **`void display()`**.

```java
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

## ⚠️ The Problem

But what is the problem with this? Let's assume in the future we had more classes. This was **`testClass1`**. This was **`testClass2`**. Let's assume we also had **`testClass3`**. So all of them had already implemented **`show`**. Let's write here "testClass1 Showing", "testClass2 Showing", "testClass3 Showing".

Now in the future, when a **`display`** method comes in, the problem is that now you have to go into every class and implement this **`void display()`** as well. Otherwise, an error will come. It will say that this is an abstract method and you have to go to every single class and implement it wherever you have implemented this interface.

---

## 💡 The Solution

To avoid this, what can you do? Here you can simply use a **`default`** keyword and write its definition right here. If its definition is common, right here write **`System.out.println("Default Display Method");`**.

> Using the **`default`** keyword is mandatory. Because of this, what will happen is that you won't need to go into every class and override this **`display`** method.

```java
interface test {
    void show();

    default void display() {
        System.out.println("Default Display Method");
    }
}

class testClass1 implements test {
    public void show() {
        System.out.println("testClass1 Showing");
    }
}

class testClass2 implements test {
    public void show() {
        System.out.println("testClass2 Showing");
    }
}

class testClass3 implements test {
    public void show() {
        System.out.println("testClass3 Showing");
    }
}

```

---

## ⚙️ Execution & Proof

Now look what happens. I did **`testClass1 obj = new testClass1();`** and if I do **`obj.show()`** it will be called. Look, "testClass1 Showing" is happening.

And now look at an interesting thing. You can also call **`obj.display()`** now. Right? Look, this is an object of **`testClass1`**. In **`testClass1`**, look, there is no **`display`** method. But it is implementing this interface and this is a default method. So this **`display`** method will also be accessible.

So now when I run it, the **`display`** method will also be called. "testClass1 Showing" was called. Now "Default Display Method" also got called.

```java
class Main {
    public static void main(String[] args) {
        testClass1 obj = new testClass1();
        obj.show();
        obj.display();
    }
}

```

---

## 🧠 Deep Dive into the Concept

Let's dive a little deeper and understand why default methods were brought in. Like this is an interface. Interfaces only have abstract methods. So if any class implements this interface, it will have to implement these abstract methods.

```text
interface test {
    void show();
    
    default void display() {
        s.o.p.. ("Disp..");
    }
}
---------------------------------------------------------
Class A implements test {   | Class B implements test { | Class C implements test {
                            |                           |
    void show() { ... }     |     void show() { ... }   |     void show() { ... }
                            |                           |
}                           | }                         | }

```

* For example, look here is a class, **`Class A`**. It has implemented the **`test`** interface. So it will have to define this **`show`** method here.
* Similarly, look at **`Class B`**. It has also implemented **`test`**. It will also have to implement the **`show`** method.
* Similarly, **`Class C`** will also have to implement the **`show`** method.

And if we assume in the future, for some reason, you needed to add one more abstract method here, then you know what the problem is? You will have to go to every class and define this **`display`** method as well. Right? You'll have to implement it. Add the **`display`** method here, then go here as well and add the **`display`** method.

So to avoid so much hassle, what did Java do? It said that if you don't want to define this **`display`** method in every class, then define it with the **`default`** keyword.

**`default void display()`** and you define its body here. There is no need to go to every class and define it. Its body, if the definition here is common, then define it right here with the **`default`** keyword. Let's write anything here: **`System.out.println("Disp..");`**.

> Now what will happen is that let's assume you made an object of **`Class A`**:
> **`A obj = new A();`**
> You can call **`obj.show()`** because it is obvious you have implemented **`show`** here, but now you can also call **`display`**: **`obj.display()`**.

Although look, **`display`** is not visible to you inside this **`Class A`**, but it is here inside this interface. But since we have implemented this interface, we can now access this default method directly too. So, **`obj.display()`** will also work.