# 🚀 Stream Reuse Trap

## 🛠️ The Code and The Trap

I have taken a simple list of integers here: **1, 2, 3, 4**. With its help, I created a **Stream** of integers. I used `list.stream()`. Now you can apply whatever operations you want on the stream. For example, I did `stream.count()`, so here we will get the count. How many elements are in this list? I printed the total elements. After that, we are also printing all the elements: `stream.forEach(System.out::println)`.

Pause and think, if I run this entire code, what will be the output?

```java
public class Test {
    public static void main(String[] args) {
        List<Integer> list = List.of(1, 2, 3, 4);

        Stream<Integer> stream = list.stream();

        long count = stream.count(); //.collect(Collectors.toList())

        System.out.println("Total elements = " + count);

        System.out.println("Elements = ");

        stream.forEach(System.out::println);
    }
}

```


The expectation is that the total count of elements will be printed here—there are a total of four elements—and after that, all the elements will be printed: **1, 2, 3, 4**. Let's run it once and see.

```text
Total elements = 4
Elements = 
Exception in thread "main" java.lang.IllegalStateException: stream has already been operated upon or closed
	at java.base/java.util.stream.AbstractPipeline.sourceStageSpliterator(AbstractPipeline.java:279)
	at java.base/java.util.stream.ReferencePipeline$Head.forEach(ReferencePipeline.java:658)
	at javaDopamineYouTube.Test.main(Test.java:17)

```


So look, the total elements got printed here. After that, when we went to print all the elements, an `IllegalStateException` occurs. What is it saying? `stream has already been operated upon or closed`.

---

## 🧠 The Concept

Do you know what this error means? When you defined a stream here, and as soon as you applied a terminal operation on it—here, `.count()` is a terminal operation, or `.collect()` is also a terminal operation.

> **Aha! Moment:** Whenever you apply a terminal operation to a stream, you cannot use that stream again after that. You have to create a new stream.

That is why look at the mistake we made here. We applied a terminal operation to the stream here. Now this stream is finished. After this, you are using the same stream again. That is why it is saying this stream has already been used.

## 🔧 The Solution

So either you do something like this: generate a new stream again in this same stream variable, and call it again. Then it will run. Look, **1, 2, 3, 4** got printed. Or you can do it like this. Instead of using `stream` here, do `list.stream()`. So a new stream is created here, and we called `forEach` on it. So even now it will run. Look.

```java
public class Test {
    public static void main(String[] args) {
        List<Integer> list = List.of(1, 2, 3, 4);

        Stream<Integer> stream = list.stream();

        long count = stream.count(); // .collect

        System.out.println("Total elements = " + count);

        System.out.println("Elements = ");

        list.stream().forEach(System.out::println);
    }
}

```


```text
Total elements = 4
Elements = 
1
2
3
4

```


---

## 🔍 Background Details

Now let's go into the background and see in detail what actually happened here. A stream just gives you a vision, a view.

For example, let's say I applied a filter in the stream here. Let's say I applied a filter that I only want to see odd numbers: `x -> x % 2 != 0`, or I only want to see even numbers. So I applied this filter logic of the stream, and through this logic, if you look, you will only see odd numbers. Consider this as a kind of glasses or a view, and this is you looking from here, so you are only seeing even numbers. Two and four would be visible. Right?

```text
      👁️ (You / Viewer)
             |
             V
      ~~~~~~~~~~~~~~~~~~~~~~~~  <-- Filter View: .filter(x -> x % 2 == 0)
             |
             V
       { 1, 2, 3, 4 }           <-- Elements (2 & 4 match the filter)
       
       [ termin: • count ]      <-- Terminal Operation

```


And as soon as you apply a terminal operation to this stream, like let's say you applied `.count()`, which is a terminal operation. After that, what happens is that the work of this stream is finished, and then this stream is destroyed. As soon as you applied any terminal operation to it, because a stream does not store data. It just gives a view, it is used for processing. Data is not stored in it.

## 🛑 Terminal vs Intermediate Operations

So what terminal operations do we have available today?

* `count()`
* `forEach()`
* `collect()`
* `reduce()`
* ...and so on.

Yes, you can apply many intermediate operations in between. Like `list.stream()`, you applied some filter in it: `filter(x -> x % 2 == 0)` meaning you only want to see even numbers. Then let's say you applied `.sorted()`. You want those numbers to be seen in a sorted fashion. Then finally, you applied these intermediate operations.

Then finally, to finish it, you apply a terminal operation. In the terminal operation, apply `count()` or anything.

```java
list.stream()
    .filter(x -> x % 2 == 0)
    .sorted()
    .count()  // <-- Terminal Operation

```

So as soon as you applied the terminal operation, the usage of this stream is done. Now this stream is finished. You cannot use this same stream again. Whatever stream you had created. You can no longer use this stream. You will have to create a new stream.