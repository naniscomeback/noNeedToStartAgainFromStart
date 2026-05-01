# Understanding Combinations and Pascal's Triangle

## 1. What is \(nCr\) really?
Imagine you have a bag with 3 colored balls: Red (R), Blue (B), and Green (G). You want to pick 2 balls.

In math, we call the total number of items \(n\) (\(n=3\)) and the number you pick \(r\) (\(r=2\)).

**\(nCr\)** is just a shortcut way of asking: "How many different pairs can I pull out?"

If you reach in, you could get:
- Red and Blue
- Red and Green
- Blue and Green

That’s it! There are only 3 ways. So, **3C2 = 3**.

> **Note:** In combinations, Red+Blue is the same as Blue+Red. We only care about what's in your hand, not which one you grabbed first.

---

## 2. How does this make Pascal’s Triangle?
Pascal’s Triangle is a "cheat sheet" of these answers. Let’s build it by "picking things":

### Row 0:
- You have 0 things, pick 0.
- There is only 1 way to do nothing.
- **Top row: 1**

### Row 1:
- You have 1 thing.
- Pick 0: **1 way**
- Pick 1: **1 way**
- Next row: **1, 1**

### Row 2:
- You have 2 things.
- Pick 0: **1 way**
- Pick 1: **2 ways** (like picking just Red or just Blue)
- Pick 2: **1 way** (picking both)
- Row 2 is: **1, 2, 1**

If you keep going, the triangle "grows" because you are adding up the choices from the row above.

---

## 3. Why is the triangle "The Logic"?
The "magic" rule of Pascal's Triangle is:	Each number is the sum of the two above it.

### The Beginner Logic:
to get to a certain number in the triangle, think of a "Path." To get there from the top, you're counting how many different "paths" lead there.
down steps = \( n \)
r steps to the right = \( r \)
nCr = just a fancy counting tool so you don't have to draw or list out colors every time!
