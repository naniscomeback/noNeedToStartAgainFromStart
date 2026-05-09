# Longest Subarray with Given Sum K (Only Positive Numbers)

## Problem Statement

Given an array `nums` of size `n` and an integer `k`, find the **length of the longest subarray whose sum is equal to `k`**.

If no such subarray exists, return `0`.

---

# Examples

## Example 1

```python
Input:  nums = [-1, 1, 1], k = 1
Output: 3
```

Explanation:
- Entire array sums to 1

---

## Example 2

```python
Input:  nums = [10, 5, 2, 7, 1, 9], k = 15
Output: 4
```

Explanation:
- Subarray: [5, 2, 7, 1]

---

# 1. Brute Force Approach

## Idea

Try all possible subarrays and calculate their sum.

---

## Algorithm

1. Pick a starting index `i`
2. Pick an ending index `j`
3. Compute sum of subarray `arr[i...j]`
4. If sum == k → update maximum length

---

## Code

```python
class Solution:

    def longestSubarray(self, nums, k):

        n = len(nums)
        maxLength = 0

        for start in range(n):

            for end in range(start, n):

                currentSum = 0

                for i in range(start, end + 1):
                    currentSum += nums[i]

                if currentSum == k:
                    maxLength = max(maxLength, end - start + 1)

        return maxLength


nums = [-1, 1, 1]
k = 1

obj = Solution()

print(obj.longestSubarray(nums, k))
```

---

## Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N³) |
| Space Complexity | O(1) |

---

## Why This is NOT Good

### 1. Triple nested loops

Very slow.

---

### 2. Recomputing sum repeatedly

Same subarray sum is calculated multiple times.

---

# 2. Optimal Approach (Sliding Window / Two Pointers)

## Key Idea

Since all numbers are **positive**, we can safely use sliding window.

---

# Why Sliding Window Works Here

Because:

```text
Adding elements → sum increases
Removing elements → sum decreases
```

So we can adjust window dynamically.

---

# Algorithm

1. Initialize:
   - `left = 0`
   - `right = 0`
   - `sum = nums[0]`
2. Expand window using `right`
3. If sum > k:
   - shrink window using `left`
4. If sum == k:
   - update maximum length
5. Repeat until end of array

---

# Code

```python
class Solution:

    def longestSubarray(self, nums, k):

        n = len(nums)

        left = 0
        right = 0

        current_sum = nums[0]

        maxLen = 0

        while right < n:

            # shrink window if sum too large
            while left <= right and current_sum > k:
                current_sum -= nums[left]
                left += 1

            # check valid condition
            if current_sum == k:
                maxLen = max(maxLen, right - left + 1)

            # expand window
            right += 1

            if right < n:
                current_sum += nums[right]

        return maxLen


nums = [10, 5, 2, 7, 1, 9]
k = 15

obj = Solution()

print(obj.longestSubarray(nums, k))
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(1) |

---

# Why This Approach Works

## 1. Positive numbers only

So sum behaves predictably:

- Increase when moving right
- Decrease when moving left

---

## 2. No recomputation

Each element is visited at most twice.

---

## 3. Efficient window adjustment

We never restart from scratch.

---

# Dry Run

## Input

```python
[10, 5, 2, 7, 1, 9], k = 15
```

---

## Steps

| Step | Window | Sum | Action |
|---|---|---|---|
| 1 | [10] | 10 | expand |
| 2 | [10,5] | 15 | valid → maxLen = 2 |
| 3 | [10,5,2] | 17 | shrink |
| 4 | [5,2,7,1] | 15 | valid → maxLen = 4 |

---

## Answer

```python
4
```

---

# Important Constraint Note

This sliding window approach ONLY works when:

```text
All elements are positive
```

---

# If Array Contains Negatives

Then sliding window breaks.

You must use:

- Prefix Sum
- Hash Map

---

# Interview Insight

This problem tests your understanding of:

## 1. Brute force → intuition
## 2. Sliding window → optimization
## 3. Constraint awareness

---

# Common Mistakes

## 1. Using sliding window with negative numbers

❌ Incorrect assumption

---

## 2. Recomputing sum every time

❌ Leads to O(N²) or O(N³)

---

## 3. Forgetting window shrink condition

```python
while sum > k:
```

is critical.

---

# Key Learning

Whenever you see:

```text
Longest subarray + sum condition + positive numbers
```

Immediately think:

```text
Sliding Window / Two Pointers
```

It is one of the most important patterns in array problems.
