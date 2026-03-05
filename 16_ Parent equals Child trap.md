# 🚀 Parent equals Child trap


## 🛠️ The Code Setup

I have defined a simple **Parent** class. It has two methods: `void show()` and `void display()`. Similarly, I have defined a **Child** class here which is inheriting this **Parent** using the `extends` keyword. It has its own `void show()` method. What does this mean? It has overridden the `show()` method of the parent. And it also has its own method named `childMethod()`.

I have created an object of **Child** and stored it in a **Parent** reference type variable. Why is this valid? Because this is a parent and this is a child. So you can store a child's object in a parent type reference variable. So this is a perfectly valid statement.

After this, let's see, I have called `show()` on the same object. I have called `display()` on the same object. I have called `childMethod()` on the same object. So pause and think what the output of these three lines will be?

```java
class Parent {
    void show() {
        System.out.println("Parent show method");
    }
    void display() {
        System.out.println("Parent display method");
    }
}

class Child extends Parent {
    void show() {
        System.out.println("Child show method");
    }
    void childMethod() {
        System.out.println("Child childMethod");
    }
}

class Main {
    public static void main(String[] args) {
        Parent obj = new Child();

        obj.show();
        obj.display();
        obj.childMethod();
    }
}

```

---

## 🐛 The Error and Execution

So look, what is the error on running? `obj.childMethod() cannot find symbol`. What does this mean? It means `obj.show()` must have been called here, there was no error. There was no error in `obj.display()` either. The error is coming on `obj.childMethod()`.

So if I comment this out, let's see, the rest should run. `obj.show()` will be called. So you see, for the parent's show, the child's `show` method was called. Why? Because here the actual object is of the child. So when I called `show` on it, since the child has overridden the `show` method, the child's method will be called.

After that, when I called `obj.display()`, look, there is no `display` method in the child, but it has inherited the parent, so the parent's `display` method can be called, so here the parent's `display` method was called.

But why is this problematic? Why is `obj.childMethod()` not able to be called when the object is actually of the child and this `childMethod` is also defined here in the child? Let's see what is actually happening in the background, why we are getting this error.

```java
class Parent {
    void show() {
        System.out.println("Parent show method");
    }
    void display() {
        System.out.println("Parent display method");
    }
}

class Child extends Parent {
    void show() {
        System.out.println("Child show method");
    }
    void childMethod() {
        System.out.println("Child childMethod");
    }
}

class Main {
    public static void main(String[] args) {
        Parent obj = new Child();

        obj.show();
        obj.display();
        //obj.childMethod();
    }
}

```

---

## 🧠 The Concept: Reference Type vs Object Type

So remember one thing that whenever we define it like this, for example, `Parent obj`... here **Parent** is called the **Reference Type**. What is `obj`? It is my variable. And what is its type? It is **Parent**. Meaning it is also called the reference type.

So look, the reference type is of **Parent**. And the actual object is of **Child**. We have created a **Child** type object.

```text
[Reference Type]              [Object Type]
+--------+                  +--------------+
| Parent |       new        | Child Object |
|  obj   | ---------------->|              |
+--------+                  +--------------+

```

So always remember a rule regarding which methods can be called. Who decides that? The reference type defines it. It decides. Which methods can be called? The reference type, whatever it is, will decide that.

My reference type is of **Parent**. Now as soon as I called `obj.show()`, look, `show` is visible to the parent because if you look inside the parent class, `show` is there. But when we call `obj.show()`, at runtime the compiler sees that okay, the child has overridden this, and the actual object is of the **Child** type. That is why the child's `show` method is called. This thing is decided at runtime. This is also called **runtime polymorphism**.

After that, when `obj.display()` was called, look, `display` is present in the parent class. Okay, great. Has the child overridden `display`? No, it hasn't. So during runtime, it will see that okay, the child hasn't overridden this `display`. So we will call this `display`. So look, this one will be printed: `Parent display method`.

When we called the third method, and called this line `obj.childMethod()`, look, the parent doesn't even have a `childMethod`. It only has `show` and `display`. So it is not even visible to the parent where the `childMethod` actually is. Right? That is why we got an error on this line.

So what did I just... I am repeating again that which methods can be called, who decides that? It should be visible to your reference type. That method should be accessible. Whereas here there is no method named `childMethod` with this parent. That is why a compilation error occurred.

---

## 🎯 The Ultimate Rule

And ultimately when you make a call, like when you called `obj.show()`, `show` is visible to the parent. Right? So that is why this is a valid line. But when we run it, then during runtime the compiler sees that okay, which `show` is actually supposed to be called? Should this `show` be called which the parent has, or should this `show` be called? So the compiler looks at what type the object is. The method of whatever type the object actually is will be called in the end. That is why this `show` will be called because the object was of the **Child** type.

So just remember a simple rule forever:

> **The Golden Rule**
> * **What methods can be called** ➔ Decided by the **Reference Type**
> * **What methods actually run** ➔ Decided by the **Object Type**
> 
> 

So the reference type here was **Parent**. So let's go and look in the **Parent** class. Here we have a `show` method and a `display` method. This means the `show` and `display` methods can be called. So look here I have called the `show` and `display` methods.

And who actually runs? Which method will run? Will that parent's method run or will the child's method run? That depends on the object type, what the actual object type is.

The `show` method is available in the parent. This method, this `display` call, this is also valid because the `display` method is also available. And `childMethod` is not available in the parent class at all. That is why this became invalid.

The compiler will tell you at compile time itself. When you write this, the compiler will tell you at compile time itself that no, you cannot make this call because the `childMethod` is not accessible to the parent and you have defined the reference type as **Parent** here and the parent does not have access to the `childMethod`. Right?

Now when you remove this, when you run it, then during runtime, this `show` method that you have called here, what type is this object actually? The method of whatever type it is will be called. That is why the child's `show` was called here, and when it came time to call the `display` method here, it saw that the child has no `display` method, so that `display` method is in the parent, so the parent's `display` will be called.
