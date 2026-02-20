# 🚀 Labeled vs Unlabeled Break Statements
---

## 🧠 The Trap: Breaking Out of Nested Loops

Look here, there is a simple double **for loop**. **i** is going from 1 to **i** < 10. Here **j** is going from 1 to **j** < 10. And let's assume I have to apply a condition that if **i** == 2 AND **j** == 5... It can be any kind of condition. So what do I have to do? I need to break, but break from the *entire* **for loop**. From the inner one and from the outer one too. Meaning, exit completely from the double **for loop**.

So what will you do for that? First, when you apply the **break** statement, you will only exit from the inner **for loop**, right? Then to go outside, you will have to keep a variable here.

You would make a **boolean breakOuterForLoop = false**, and as soon as this statement comes, this condition comes, mark it as **true**. Then as soon as you exit the inner **for loop**, put a check here: *Have I exited this for loop? Is this true?* If it becomes true, meaning I have to exit the outer **for loop** as well, then now I will break. So when I apply the break statement here, see it is inside the outer **for loop**, so this will also break, and then we will come out.

```java
public class Main {
    public static void main(String[] args) {
        
        boolean breakOuterForLoop = false;
        for(int i = 1; i < 10; i++) {
            
            for(int j = 1; j < 10; j++) {
                
                if(i == 2 && j == 5) {
                    breakOuterForLoop = true;
                    break;
                }
            }
            
            if(breakOuterForLoop == true) {
                break;
            }
        }

```

Now the question is, this separate variable I have to take to exit the outer loop—from the outermost loop—can I avoid this? Can I exit the entire double **for loop** at once from right here? Pause the video and think about how we can do it.

---

## 💡 The Concept: Java Labels

Okay? So now I will tell you that there is a concept called a **label** in Java. Right? What is a label? How do we write it? Look at that.

You can keep any name for the label. For example, let's assume I kept the name **Nilesh** here and gave a colon here. Do you know what this means?

> I am saying that this entire block, this big block, comes under this label.

Now you can give it any name. Let's assume I named it **outerLoop**. Right? So this became the label for this entire **outerLoop** block.

---

## 🛠️ The Code: Labeled Break Statement

Now look what I will do. I don't need to keep an extra variable to go out of the entire loop. Remove all of this. Just simply here, as soon as **i** == 2 and **j** == 5 happens. You were writing **break** here earlier, right? Now what I will do is, after **break**, I will also write that I actually want to exit this outer loop as well.

This label, what is this label representing? It is representing this entire block statement. So with **break**, you are telling Java, *"Hey, what do I need a break from? This outer loop label represents all of that, I need a break from all of them."* So it will break from all of them and come out directly. Right?

So at once, see, you exited the inner loop and exited the outer loop too, by using this **break** tag. And you can name this tag anything. Keep it **Nilesh** here. Right? And write **Nilesh** here.

```java
public class Main {
    public static void main(String[] args) {
        
        Nilesh:
        for(int i = 1; i < 10; i++) {
            
            for(int j = 1; j < 10; j++) {
                System.out.println(i + " " + j);
                if(i == 2 && j == 5) {
                    break Nilesh; //labeled break statement
                }
            }
        }

```

---

## 💻 Output Execution

So let's do one thing. Let's run this **for loop** once and see. I will put a print statement here. **i** and **j** will be printed here. So look here, what is printing?

For 1, the whole thing got printed (1 to 9). As soon as my 2 and 5 printed... Look, as soon as my **i** and **j** printed 2 and 5, right here we broke. So we exited the entire **for loop**.

**Terminal Output:**

```text
1 1
1 2
1 3
1 4
1 5
1 6
1 7
1 8
1 9
2 1
2 2
2 3
2 4
2 5

```

So I hope you understood this.

---

## 🎙️ Interview Tip

And remember one thing, this is called a **labeled break statement**.

> So a question can come in an interview to trick you: *What is the difference between a labeled break statement and an unlabeled break statement?* This is a **labeled break statement** because look, after **break** I am using a label. And if I don't put it here, then this becomes an **unlabeled break statement**.