# 🚀 Stream filter() Trap
---

## 🛑 The Trap

I have taken a simple list which has 1, 2, 3, 4, 5, 6. And I applied a stream on it and filtered it out. Who did I filter? Those numbers which are even. Meaning whose $x \bmod 2 == 0$. I am only keeping those in this list.

So after this filter is applied to this list collection, I have printed it. Now you have to tell me which numbers will be printed. Obviously, I have only kept the even numbers here, so the expectation is that only even numbers will be printed.

```java
public class Test {
    public static void main(String[] args) {

        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6);

        list.stream()
            .filter(x -> x % 2 == 0);

        System.out.println(list);
    }
}

```

Output: `[1, 2, 3, 4, 5, 6]`.

So look, what is the reason for this? The `list.stream().filter()` that we applied, it does not modify the actual collection. We applied it to the list collection here. It does not modify it. This `stream().filter()` just tells you that I have given you a way through which only even numbers will be visible to you. But it hasn't picked up those even numbers and put them anywhere yet.

---

## 🧠 The Concept

Stream just gives you a view. It gives you a perspective that yes, if you look at the list from this perspective, you will only see even numbers.

> So understand stream as a kind of glasses which, when you wear them, you only see even numbers.

We haven't taken any action on it yet. We can see the even numbers, but we haven't picked them up and put them anywhere yet.

*Imagine you are an observer looking through a "Pipeline/view" (like a pair of glasses). The logic inside is `(x -> x % 2 == 0)`. On the other side of this pipeline are the numbers 1, 2, 3, 4, 5, 6. Through these glasses, the odd numbers are crossed out, and you only see 2, 4, 6.*

```text
                  Pipeline/view
                       \
                       /
     \ | /             \
    .-' '-.            /
   /       \           \          1, 2, 3, 4, 5, 6
  |    O    >          /          x     x     x
   \       /           \
    '-...-'            /
                       \
               (x -> x % 2 == 0)

```

Let's dive a little deeper and see what is actually happening in the background with this `stream().filter()`. I can explain this very well with an example. Like the list we just defined. Right now, you can see it normally. Let's assume this is you, and you can see it, and you can see all the numbers.

Now when you define a stream, stream doesn't do anything. It creates a view for you. View means, consider it a mirror, which in technical terms you can also call a pipeline, or you can call it a view. Or if I say it in very normal language, it's a kind of glasses. If you put them on your eyes, you will only see the numbers here according to the logic of this filter.

So what did we put in the filter? That $x \bmod 2 == 0$ should be true. Meaning, I applied this filter that if I look through these glasses, through this filter, I should only see even numbers. So now if you look at it through this stream, you will only see even numbers. You won't be seeing 1 right now. You won't be seeing 3 right now. You won't be seeing 5. You will only be seeing 2, 4, 6. Okay? So stream just gives you a view.

---

## 💡 The Solution

Now it has given a view, but right now you are not doing much with these even numbers. You are not collecting them. So to collect them, you have to apply **Terminal Operations**. Until you apply a terminal operation, the data will not be collected.

So to pick them up and put them somewhere, what will we do? We will do `.toList()`. That is, now it will make a list and give it to me, and I will store it here in **result**. Now I will print this **result**. So look, I will only see even numbers in this.

```java
public class Test {
    public static void main(String[] args) {

        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6);

        List<Integer> result = list.stream()
            .filter(x -> x % 2 == 0)
            .toList();

        System.out.println(result);
    }
}

```

You see? Now `[2, 4, 6]` is printing.

---

## ⚙️ Terminal Operations & Lazy Evaluation

*Visual explanation: To get a result like `result = list.stream().filter(num -> num % 2 == 0).toList();`, you must end the stream with terminal operations. Examples include:*

* *.toList()*
* *.collect()*
* *.forEach()*
* *.count()*

Now what does terminal operations mean? Like what I just taught you, it could be `.toList()`, or you can apply `.collect()`, or you can apply `.forEach()`, or you can apply `.count()`. You can apply these kinds of things. Okay? So these are all terminal operations. Until you apply these, those data won't be collected. No action will be taken on it. As soon as you apply a terminal operation, an action will be taken on it, and then you will get the data. Okay? And what did we apply here, remember? We applied `list.stream().filter()`. So after that, I applied `.toList()` and we stored it in the result.

*Methods like `.filter()`, `.map()`, and `.sorted()` simply create a "view". This underlying concept is known as "Lazy Evaluation."*

So actually what happens, I will tell you a very important thing. It might even be asked in an interview. These operations I told you about, like `stream().filter()` or `stream().map()` or `stream().sorted()`, these guys just give you a view. Okay, they don't actually bring any changes to your data. If you want that data through this view that you are seeing, then you will have to apply a terminal operation which I told you about here.

Actually, there is a very important term used, that streams follow **Lazy Evaluation**. Many people also say Streams are Lazy Evaluated.

> What does this mean? It will not take action until you have applied a terminal operation. It just gives you a view and leaves it.

If you hadn't applied a terminal operation here, let's say you hadn't applied `.toList()`, and just left it like that, then nothing. It's just a view created. That's it. And nothing else is happening. Story over, nothing is happening to it. So if you also want the data of this view, what data is being received through this view, for that you have to apply a terminal operation.