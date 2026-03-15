# 🚀 findFirst() Stream Trap

## Problem Setup

I have simply taken a list of integers here. By using `list.stream()`, I have filtered out those that are even numbers. And here I am also printing out which numbers I am checking. Like here it will be checking 1. Then checking 2. Checking 4, checking 6, checking 8. And when I get an even number, we keep filtering them out; we only want the even numbers. Then which are the even numbers here? There is 2, 4, 6, 8. And from there I want to find the first element. Meaning, I want the answer to come out as 2. That is, whatever was the very first even number I got among the even numbers. Then finally, whatever new list has been created here, I am printing it here.

## 🛠️ The Code

```java
public class Test {
    public static void main(String[] args) {
        List<Integer> list = List.of(1, 2, 4, 6, 8);

        Optional<Integer> newList = list.stream()
            .filter(x -> {
                System.out.println("Checking: " + x);
                return x % 2 == 0;
            })
            .findFirst();

        System.out.println(newList);
    }
}

```

Pause and think what output should be?

---

## 🔍 Analyzing the Output

So if I run this, what will happen? It did "Checking: 1". It was the first element of the list. Then it did "Checking: 2". It was the second element of the list. After that, it stopped. Then finally, it printed what the new list is. The new list is 2, which was also expected. I wanted to get the very first integer that is an even number. But it didn't even check all the numbers. It only checked up to 2 and stopped.

**Terminal Output:**

```text
Checking: 1
Checking: 2
Optional[2]

```

So what actually happened here is that as soon as this `findFirst()` executed, it told the stream, "As soon as you find the first number, just tell me and stop right there."

> "As soon as you find the first number, just tell me and stop right there."

That is why, as soon as it checked 1, this is an odd number, so this condition became false. After that, it checked 2, so this is an even number. As soon as the condition became true, the stream stopped right there and that 2 was stored in the new list and that is what is printing here.

---

## ⚙️ Background Mechanics: Short-Circuit Evaluation

Let's look in the background and understand what is actually happening here.

* Java actually stopped after finding the first match.
* As soon as it found the first match, what is this check for? It is for an even number.
* As soon as it got the first match, it never even looked at 4, 6, or 8.
* As soon as the first match was found in 2, it stopped at that very moment.

> **"Short-circuit evaluation"**

This is called short-circuit evaluation.

> "`findFirst()` doesn't need the full result. So, the stream stops as soon as it finds one match"

This happened because of `findFirst()`. Short-circuit evaluation occurred. As soon as the first result was found here, the first even number, the stream stopped right there and we just printed the output here.

---

## 📋 Other Similar Methods

So `findFirst()` is not the only one. There are others like this that you will find.

**Examples:**

* **`anyMatch()`**
* **`allMatch()`**
* **`noneMatch()`**
* **`findAny()`**

It was simple, but it's possible that many people get confused.