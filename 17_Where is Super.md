# 🚀 Where is Super?

## 🧠 The Problem Statement

We have written a `Parent` class which has its own constructor. Here, a `Child` class is written which extends `Parent`, meaning it inherits it. `Child` has its own default constructor and `Child` also has its own parameterized constructor.

And look here, I have written `this(10)`. Do you know what you can do with the help of `this`? You can call any constructor within this class. For example, here I have used `this(10)`. Because of this `10`, Java understands that this specific constructor needs to be called because the `10` parameter will be passed into it. Right? So, you can also call constructors in this manner.

## 🛠️ The Initial Code

```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}
class Child extends Parent {
    Child() {
        this(10);
        System.out.println("Child Default Constructor");
    }

    Child(int val) {
        System.out.println("Child Parameterised Constructor");
    }
}
class Main {
    public static void main(String[] args) {
        Child obj = new Child();
    }
}

```

---

## 🔍 The Hidden `super()`

So my question is, when I create this `Child` object, We know from earlier that whenever we create a child object, and if that child has inherited a class—meaning the parent it has inherited must already be created. For that, Java has provided us with the `super` keyword. If you do not write the `super` keyword, Java writes the `super` keyword by itself. You might not be able to see it here, but internally it would have written it for you.

My question to you is, when I create this `Child` object, where will Java write the `super` keyword? Will it write it on the first line of this constructor? Here, or will it write it on the first line of this other constructor?

First, let me run it once to show you that there are no mistakes in this code. But you need to figure out that the `Parent` constructor has indeed been called. This means that the `super` keyword must have been written somewhere. Where was it written?

> **Key Rule:** Just as the `super` keyword must be the very first line inside a constructor, similarly, the `this` keyword must also be the very first line inside any constructor.

So when this `Child` object is created, my execution flow goes here. Then, as soon as this `this` keyword is seen, our flow goes here. Since there is no `this` keyword here, Java inserts `super` here. So, actually, `super` would have been inserted right here. If you were to insert `super` in the first constructor, obviously it would be wrong. You would get a compilation error. Why will it come? Because I just told you that the `this` keyword must always be the first line of the constructor. That is why Java did not insert it there, but inserted it here.

## 🛠️ The Code with Explicit `super()`

```java
class Parent {
    Parent() {
        System.out.println("Parent Constructor");
    }
}
class Child extends Parent {
    Child() {
        this(10);
        System.out.println("Child Default Constructor");
    }

    Child(int val) {
        super();
        System.out.println("Child Parameterised Constructor");
    }
}
class Main {
    public static void main(String[] args) {
        Child obj = new Child();
    }
}

```

---

## 🔬 Behind the Scenes Execution Flow

So let's see what is actually happening behind the scenes.

> **Thumb Rules:**
> * `"this" must be the first line in the constructor`.
> * For example, if you are writing `this` here, it must always be the first line of the constructor; nothing should be written before it. 
> * `"super" must be called at the first line in the constructor`.
> * I had already told you this, that `super` also needs to be called on the first line of the constructor because the parent must always be built before creating the child object.
> 
> 

So obviously, the compiler cannot insert `super` here. Therefore, our flow will go here; because of `this`, this constructor will be called. Then Java will see that, okay, the `this` keyword is not used here, so it will simply insert `super` here.

### 🔄 Execution Flow Breakdown

So how does our flow actually work?

1. First, I created the `Child` object here. `new Child();`
2. After this, our flow went here to this `Child` constructor. `Child() { ... }`
3. Then, as soon as it saw that `this` is called, it came here. Flow moves from `this(10);` to `Child(int val)`
4. Then it inserted `super` here, and because of `super`, the parent constructor was called. Flow moves from `super();` to `Parent() { ... }`
5. After that, the `Child` parameterized constructor was called further.
6. Then the flow went back here, and the `Child` default constructor was called.

**ASCII Representation of the Execution Flow:**

```text
Main.java execution
│
└──> new Child()
        │
        └──> Child()
                │
                └──> this(10)
                        │
                        └──> Child(int val)
                                │
                                └──> super()
                                        │
                                        └──> Parent()

```

---

## 🎯 The Ultimate Rule

So, you can keep this rule in mind like this:

> **Rule:** `JAVA inserts super() into the constructor that does not call this()`

Meaning, wherever `this` is not being called, Java inserts `super` there. Because what does `this` already say? The `this` keyword already says, "Hey, I need to be on the first line." And `super` also has the same requirement, that you must write it on the first line as well. So, `this` was already present there, which is why `super` came here instead.