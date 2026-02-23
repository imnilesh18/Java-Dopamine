# 🚀 ArrayList Size Trap
---

## 💻 The Problem

Look, I have defined a simple main method here, and inside it, I have defined an **ArrayList** named **list**. Look at its initial size, I have kept it as 10. And here, I am printing **list.size()**. So, think, what will be the output of this?

```java
public class Main {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>(10);

        System.out.println(list.size());
    }
}

```

Look, the output will be **0**.

Now understand why the answer is zero. Even though, as you can see, I kept its size as 10 here. But why is it showing zero when finding the size here?

---

## 🧠 The Concept & Inner Workings

So, what actually happens? When you define an ArrayList and you provide an initial size here, it defines the **capacity**—that is, how much capacity of elements this ArrayList can store without (or before) resizing.

And if you go to its definition, let's go inside it. Look, when I called the ArrayList constructor and passed the initial capacity, it created an array of Objects. Look here, it defined an array of Objects whose initial capacity is this.

```java
public ArrayList(int initialCapacity) {
    if (initialCapacity > 0) {
        this.elementData = new Object[initialCapacity];
    } else if (initialCapacity == 0) {
        this.elementData = EMPTY_ELEMENTDATA;
    } else {
        throw new IllegalArgumentException("Illegal Capacity: "+
                                           initialCapacity);
    }
}

```

But when you go to add elements to this list. For example, let's say I did `list.add(1)`, and then I did `list.add(2)`. So now look, actually, there are two elements in it. Now if I run this, the size is coming out as **2**.

---

## 🔍 Deep Dive: The Add Method

And if you want to know in even more detail, let's go inside the implementation of this **add** method. Look what it is doing. It is calling an add method. And inside this add method, look what is happening. The **size** is getting incremented.

```java
/**
 * This helper method split out from add(E) to keep method
 * bytecode size under 35 (the -XX:MaxInlineSize default value),
 * which helps when add(E) is called in a C1-compiled loop.
 */
private void add(E e, Object[] elementData, int s) {
    if (s == elementData.length)
        elementData = grow();
    elementData[s] = e;
    size = s + 1;
}

```

So this is the size that tells you how many actual elements are in your list. `size = s + 1` is happening. So I hope this is clear to you now.

---

## 📊 Visual Summary

Let's go back here. So what did I tell you? When we define an ArrayList and initially give it some capacity, it sets the capacity. What does that mean?

> **`new ArrayList<>(10);`**
> ├── **Capacity = 10**
> │   *(How many elements it can hold without resizing?)*
> │
> └── **Size**
> *(How many elements it actually contains? Changes via `list.add()`)*

And what does size mean? Whenever you add an element, do a `.add()` or `list.add()`, then changes happen to the size. That is, how many elements it actually contains right now.

So, what does this mean?

> ### **ArrayList Capacity ≠ ArrayList Size**
> 
> 

This is the biggest test that can be taken from you in an interview. It is possible that this might be asked.