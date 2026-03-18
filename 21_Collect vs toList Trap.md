# 🚀 Collect vs toList Trap

**Collect vs toList trap**.

We have a `main` method. I have defined a list, a `List` of integers. I passed that same list through a stream, filtered out only the even numbers, and tried to create a new list using `.collect(Collectors.toList())`. So a new list will be created. It will only have even numbers. Then I passed the same list that was defined above through a stream and filtered out the even numbers. This time I used the `toList()` method. Here we have used the `toList()` terminal method. So I created a new list from here. 

When we print both, obviously `newList1` will also have even numbers. `newList2` will also have even numbers. After that, I added 10 to `newList1`. I also added 10 to `newList2`. So what should be in the output? All the even numbers, and at the end we have appended 10.

## 🛠️ The Code

```java
public class Test {
    public static void main(String[] args) {
        List<Integer> list = List.of(1, 2, 4, 6, 8);

        List<Integer> newList1 = list.stream()
                .filter(x -> x % 2 == 0)
                .collect(Collectors.toList());

        List<Integer> newList2 = list.stream()
                .filter(x -> x % 2 == 0)
                .toList();

        System.out.println(newList1);
        System.out.println(newList2);

        newList1.add(10);
        newList2.add(10);
    }
}
```

---

## 🐛 The Error

So look here, it is showing that line number 21 has failed. If I comment out line number 21 and run it now...

```java
        // ... previous code ...
        System.out.println(newList1);
        System.out.println(newList2);

        newList1.add(10);
        // newList2.add(10);
    }
}
```

---

## 🧠 The Concept

So actually, what was the issue in line number 21? What was in line number 21? It was `newList2`. What did we create `newList2` with? We created it with `toList()`. 

> **Aha!** Actually, what happens is `toList()` returns an unmodifiable list. Meaning immutable. You cannot change it. 

Whatever list `toList()` returns, we were trying to change `newList2` here. That's why we are getting a compilation error here. So let's go to the background once and see what is actually happening.

Look, this was our problem statement: we created one list using `.collect(Collectors.toList())`. The second one we created using `.toList()`. 

## 📊 Visual Explanation

```text
Java 16  -------->  toList()  --------> returns an unmodifiable list

Collectors.toList()  --------> mutable list
```

Actually, this `toList()` method was introduced in **Java 16**. The terminal method `toList()` was introduced in Java 16, and it returns an unmodifiable list. You cannot change this; now it is immutable. And `Collectors.toList()` is a mutable list. That is why we can also change it. Look at `newList1`, we created it with this. That's why it can be changed. It is mutable.

---

## 🌊 Stream Core Principle

So understand actually the principle of the stream, the core principle of the stream we used here. 

> Data flows through transformations. We apply different transformations, but it doesn't get mutated. It doesn't change. We just apply different types of transformations to it.

That is why `toList()` also follows that principle. That is, it returns an immutable list. 

## 🕰️ History of Immutability in Java

```text
Stream  ------> Data flows through transformations, it doesn't get mutated.
                So, toList() follows that principle. (returns immutable list)

Similarly,  Java 9  ------>  List.of()       ------> unmodifiable
            Java 10 ------>  List.copyOf()   ------> unmodifiable
```

And this didn't just happen with `toList()`. In the past, Java has done this correction with other methods too. 
* For example, in **Java 9**, the Java developers introduced `List.of()`, which is unmodifiable. 
* Similarly, in **Java 10**, `List.copyOf()` was introduced. This is also unmodifiable. 

So actually, what they are trying to imply here is that **immutability is the modern Java default**. So in the same way that the unmodifiable `toList()` was introduced in Java 16, similar things were done in Java 9 and Java 10 in the past.