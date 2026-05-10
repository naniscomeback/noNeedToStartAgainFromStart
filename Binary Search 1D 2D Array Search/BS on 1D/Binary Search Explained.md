# Binary Search Explained (Beginner Friendly)

# Problem Statement

Given a **sorted array** and a target element, find the index of the target.

If the target does not exist, return `-1`.

---

# Example

```python
arr = [3, 4, 6, 7, 9, 12, 16, 17]
target = 6
```

Output:

```python
2
```

Because:

```python
arr[2] = 6
```

---

# 🧠 Main Idea of Binary Search

Instead of checking every element one by one:

```text
1 → 2 → 3 → 4 → ...
```

Binary Search repeatedly divides the array into half.

---

# Real Life Analogy

Imagine searching for a word in a dictionary.

You DO NOT start from page 1.

You:

1. Open middle page
2. Decide:
   - go left
   - or go right
3. Repeat

That is Binary Search.

---

# ⚠️ Important Condition

Binary Search ONLY works on:

# ✅ Sorted Arrays

Example:

```python
[1, 3, 5, 7, 9]
```

NOT:

```python
[5, 1, 9, 2]
```

---

# Why Binary Search is Fast

Every step removes HALF of the search space.

Example:

```text
1000 elements
↓
500
↓
250
↓
125
↓
...
```

Very efficient.

---

# Time Complexity

| Algorithm | Time |
|---|---|
| Linear Search | O(N) |
| Binary Search | O(log N) |

---

# Binary Search Visualization

Array:

```python
[3, 4, 6, 7, 9, 12, 16, 17]
```

Target = `6`

---

## Step 1

```text
low = 0
high = 7
```

Middle:

```python
mid = (0 + 7) // 2 = 3
```

```python
arr[mid] = 7
```

Target:

```python
6 < 7
```

So search LEFT side.

---

## Step 2

Now:

```text
low = 0
high = 2
```

Middle:

```python
mid = (0 + 2) // 2 = 1
```

```python
arr[mid] = 4
```

Target:

```python
6 > 4
```

Search RIGHT side.

---

## Step 3

Now:

```text
low = 2
high = 2
```

Middle:

```python
mid = 2
```

```python
arr[mid] = 6
```

FOUND ✅

---

# Iterative Binary Search

---

# Algorithm

1. Set:
   - `low = 0`
   - `high = n - 1`

2. While `low <= high`:
   - Find middle
   - Compare with target
   - Move left or right

3. If found → return index
4. Else → return -1

---

# Code (Iterative)

```python
class Solution:

    def binarySearch(self, arr, target):

        low = 0
        high = len(arr) - 1

        while low <= high:

            mid = (low + high) // 2

            # Found target
            if arr[mid] == target:
                return mid

            # Search right
            elif target > arr[mid]:
                low = mid + 1

            # Search left
            else:
                high = mid - 1

        return -1


arr = [3, 4, 6, 7, 9, 12, 16, 17]
target = 6

obj = Solution()

print(obj.binarySearch(arr, target))
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(log N) |
| Space Complexity | O(1) |

---

# Recursive Binary Search

In recursion:

- function calls itself
- search space becomes smaller every call

---

# Recursive Code

```python
class Solution:

    def binarySearch(self, nums, low, high, target):

        # Base case
        if low > high:
            return -1

        mid = (low + high) // 2

        # Found target
        if nums[mid] == target:
            return mid

        # Search right half
        elif target > nums[mid]:
            return self.binarySearch(nums, mid + 1, high, target)

        # Search left half
        else:
            return self.binarySearch(nums, low, mid - 1, target)

    def search(self, nums, target):

        return self.binarySearch(nums, 0, len(nums) - 1, target)


arr = [3, 4, 6, 7, 9, 12, 16, 17]
target = 6

obj = Solution()

print(obj.search(arr, target))
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(log N) |
| Space Complexity | O(log N) |

---

# Iterative vs Recursive

| Type | Pros | Cons |
|---|---|---|
| Iterative | Faster, less memory | Slightly more code |
| Recursive | Cleaner logic | Uses recursion stack |

---

# 🧠 Important Binary Search Pattern

Whenever you hear:

```text
Sorted array
Sorted answer
Sorted search space
```

Think:

# 👉 Binary Search

---

# Where Binary Search is Used

---

# 1. Search in Sorted Array

Most basic use case.

```python
find x in sorted array
```

---

# 2. Lower Bound / Upper Bound

Used in:

- searching ranges
- insertion positions

---

# 3. First and Last Occurrence

Example:

```python
[1,2,2,2,3]
```

Find:

- first 2
- last 2

---

# 4. Search in Rotated Sorted Array

Very famous interview problem.

Example:

```python
[4,5,6,7,0,1,2]
```

---

# 5. Binary Search on Answer

Very important advanced pattern.

Examples:

- Minimum eating speed
- Allocate books
- Capacity to ship packages
- Aggressive cows

---

# 🔥 Interview Trick

Even if array is NOT sorted:

If answer space is sorted:

```text
possible possible possible impossible impossible
```

You can still use Binary Search.

This is called:

# Binary Search on Answer

---

# Common Mistakes

---

## 1. Using Binary Search on unsorted array

❌ Wrong

Binary Search requires sorted data.

---

## 2. Infinite loop

Wrong condition:

```python
while low < high
```

Correct:

```python
while low <= high
```

---

## 3. Wrong mid calculation

Correct:

```python
mid = (low + high) // 2
```

Safer in other languages:

```python
mid = low + (high - low) // 2
```

(prevents integer overflow)

---

# Beginner Memory Trick

## Binary Search means:

```text
Check middle
Throw away half
Repeat
```

---

# Key Learning

Binary Search is one of the MOST IMPORTANT algorithms in coding interviews.

You should master:

- Iterative
- Recursive
- Lower Bound
- Upper Bound
- Binary Search on Answer

These appear in almost every product company interview.
