# Count Maximum Consecutive Ones in an Array

## Problem Statement

Given a binary array containing only `0` and `1`, find the maximum number of consecutive `1`s in the array.

---

# Examples

## Example 1

```python
Input:  [1, 1, 0, 1, 1, 1]

Output: 3
```

Explanation:
- Longest streak of 1s = `[1, 1, 1]`

---

## Example 2

```python
Input:  [0, 0, 1, 1, 0, 1]

Output: 2
```

---

## Example 3

```python
Input:  [1, 1, 1, 1]

Output: 4
```

---

# Optimal Approach

## Key Idea

Traverse the array while maintaining:

- Current streak of consecutive 1s
- Maximum streak seen so far

---

# Algorithm

1. Initialize:
   - `cnt = 0` → current streak
   - `maxi = 0` → maximum streak
2. Traverse the array:
   - If element is `1` → increment `cnt`
   - If element is `0` → reset `cnt = 0`
3. Update:
   ```python
   maxi = max(maxi, cnt)
   ```
4. Return `maxi`

---

# Code

```python
class Solution:

    # Function to find max consecutive 1's
    def findMaxConsecutiveOnes(self, nums):

        cnt = 0
        maxi = 0

        for i in range(len(nums)):

            if nums[i] == 1:
                cnt += 1
            else:
                cnt = 0

            maxi = max(maxi, cnt)

        return maxi


# Driver code
nums = [1, 1, 0, 1, 1, 1]

obj = Solution()

ans = obj.findMaxConsecutiveOnes(nums)

print("Maximum consecutive 1's:", ans)
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(1) |

---

# Why This Approach Works

## 1. Single Pass Solution

We only traverse the array once.

---

## 2. Greedy Counting

We track streaks in real time instead of storing history.

---

## 3. Reset Mechanism

Whenever we see `0`:

```python
cnt = 0
```

This ensures only consecutive sequences are counted.

---

# Dry Run

## Input

```python
[1, 1, 0, 1, 1, 1]
```

---

## Step-by-step

| Index | Value | cnt | maxi |
|---|---|---|---|
| 0 | 1 | 1 | 1 |
| 1 | 1 | 2 | 2 |
| 2 | 0 | 0 | 2 |
| 3 | 1 | 1 | 2 |
| 4 | 1 | 2 | 2 |
| 5 | 1 | 3 | 3 |

---

## Final Answer

```python
3
```

---

# Why We Should NOT Use Brute Force

A brute force approach would:

- Try every subarray
- Count consecutive 1s repeatedly

This leads to:

```text
O(N²) time complexity
```

---

# Interview Insight

This problem is a classic example of:

## Pattern: "Running Counter / Sliding Window Lite"

You are basically maintaining:

- Current streak
- Best streak

No need for full window tracking.

---

# Common Mistakes

## 1. Forgetting to reset counter

Wrong:

```python
if nums[i] == 0:
    continue
```

Correct:

```python
cnt = 0
```

---

## 2. Updating max only at end

Incorrect approach:

```python
update maxi only after loop
```

Correct:

```python
update maxi at every step
```

---

# Key Learning

For problems involving:

- consecutive elements
- streaks
- continuous patterns

Always think:

```text
Maintain a running counter + reset condition
```

This is one of the simplest but most important array patterns in interviews.
