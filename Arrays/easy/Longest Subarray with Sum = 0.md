# Longest Subarray with Sum = 0

## Problem Statement

Given an array containing both **positive and negative integers**, find the length of the **longest subarray whose sum is 0**.

---

# Examples

## Example 1

```python
Input:  [9, -3, 3, -1, 6, -5]
Output: 5
```

Explanation:
Longest zero-sum subarray is:
```text
[-3, 3, -1, 6, -5]
```

---

## Example 2

```python
Input:  [6, -2, 2, -8, 1, 7, 4, -10]
Output: 8
```

Explanation:
Entire array sums to 0.

---

# 1. Brute Force Approach

## Idea

Check every subarray and compute its sum.

---

## Algorithm

1. Pick starting index `i`
2. Pick ending index `j`
3. Compute sum of subarray `arr[i...j]`
4. If sum = 0 → update maximum length

---

## Code

```python
def longestZeroSum(arr):

    n = len(arr)
    maxLen = 0

    for i in range(n):

        currentSum = 0

        for j in range(i, n):

            currentSum += arr[j]

            if currentSum == 0:
                maxLen = max(maxLen, j - i + 1)

    return maxLen


arr = [9, -3, 3, -1, 6, -5]

print(longestZeroSum(arr))
```

---

## Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N²) |
| Space Complexity | O(1) |

---

## Why This is NOT Good

### 1. Nested loops

Very slow for large arrays.

---

### 2. Recomputing sums

Same subarrays are repeatedly recalculated.

---

# 2. Optimal Approach (Prefix Sum + HashMap)

## Key Idea

If two prefix sums are equal:

```text
subarray between them has sum = 0
```

---

# Why This Works

Let:

```text
prefixSum[i] = prefixSum[j]
```

Then:

```text
sum(i+1 to j) = 0
```

---

# Algorithm

1. Initialize:
   - `prefixSum = 0`
   - `maxLen = 0`
   - HashMap `sumIndex`
2. Traverse array:
   - Add current element to prefix sum
   - If prefix sum = 0 → update maxLen = i + 1
   - If prefix sum already exists:
     → subarray found with zero sum
   - Else store prefix sum with index

---

# Code

```python
def longestZeroSum(arr):

    prefixMap = {}
    prefixSum = 0
    maxLen = 0

    for i in range(len(arr)):

        prefixSum += arr[i]

        # Case 1: from index 0
        if prefixSum == 0:
            maxLen = i + 1

        # Case 2: prefix sum repeated
        elif prefixSum in prefixMap:
            maxLen = max(maxLen, i - prefixMap[prefixSum])

        # Store first occurrence only
        else:
            prefixMap[prefixSum] = i

    return maxLen


arr = [9, -3, 3, -1, 6, -5]

print(longestZeroSum(arr))
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(N) |

---

# Why This Approach Works

## 1. Prefix Sum Insight

Same sum at two points means:

```text
everything in between cancels out → sum = 0
```

---

## 2. Efficient Lookup

HashMap gives O(1) average lookup.

---

## 3. Single Pass Solution

Only one traversal needed.

---

# Dry Run

## Input

```python
[9, -3, 3, -1, 6, -5]
```

---

## Steps

| Index | Value | Prefix Sum | Action |
|---|---|---|---|
| 0 | 9 | 9 | store |
| 1 | -3 | 6 | store |
| 2 | 3 | 9 | repeat → subarray found |
| 3 | -1 | 8 | store |
| 4 | 6 | 14 | store |
| 5 | -5 | 9 | repeat → update max |

---

## Answer

```python
5
```

---

# Why We Store Only First Occurrence

```python
if prefixSum not in map:
    map[prefixSum] = index
```

Because:

- First occurrence gives longest possible subarray later
- Overwriting would reduce answer

---

# Common Mistakes

## 1. Not handling prefixSum == 0

Wrong:

```python
only using hashmap
```

Correct:

```python
if prefixSum == 0:
    maxLen = i + 1
```

---

## 2. Overwriting hashmap values

We must store only first index.

---

## 3. Using sliding window

❌ Not valid because:
- array contains negatives
- sum is not monotonic

---

# Key Learning

Whenever you see:

```text
Longest subarray + sum condition + negative numbers allowed
```

Immediately think:

```text
Prefix Sum + HashMap
```

---

# Final Comparison

| Approach | Time | Space | Suitable |
|---|---|---|---|
| Brute Force | O(N²) | O(1) | Small input |
| Prefix Sum + HashMap | O(N) | O(N) | Best |

---

# Interview Insight

This problem teaches a very important pattern:

## “Prefix Sum + Hashing = Subarray Problems”

It is used in:

- Zero sum subarray
- Subarray with given sum
- Longest subarray problems
- Count subarrays problems
