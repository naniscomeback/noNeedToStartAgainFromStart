# Find the Missing Number

## Problem Statement

Given an array `arr[]` of size `n-1` containing distinct integers in the range `[1, n]`, one number is missing.

Find the missing number.

---

# Examples

## Example 1

```python
Input:  [8, 2, 4, 5, 3, 7, 1]
Output: 6
```

---

## Example 2

```python
Input:  [1, 2, 3, 5]
Output: 4
```

---

# 1. Brute Force Approach

## Idea

For every number from `1 to n`:

- Search it in the array
- If not found → return it as missing

---

## Algorithm

1. Compute `n = len(arr) + 1`
2. For each number `i` from `1 to n`:
   - Check if it exists in array
3. If not found → return `i`

---

## Code

```python
def missingNum(arr):

    n = len(arr) + 1

    # Check each number from 1 to n
    for i in range(1, n + 1):

        found = False

        for j in range(n - 1):

            if arr[j] == i:
                found = True
                break

        if not found:
            return i

    return -1


arr = [8, 2, 4, 5, 3, 7, 1]

print(missingNum(arr))
```

---

## Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N²) |
| Space Complexity | O(1) |

---

## Why We Should NOT Prefer This Approach

### 1. Nested Loops

For each number, we scan the entire array.

---

### 2. Very Slow for Large Input

For large `n`, performance becomes bad.

---

### 3. Inefficient Searching

We are not using the fact that numbers are in range `[1, n]`.

---

# 2. Better Approach (Hashing)

## Idea

Use a frequency array to mark presence of numbers.

---

## Algorithm

1. Create a hash array of size `n+1`
2. Mark all present elements
3. Find index with value `0`

---

## Code

```python
def missingNum(arr):

    n = len(arr) + 1

    # Hash array
    hash_arr = [0] * (n + 1)

    # Mark elements
    for i in range(n - 1):
        hash_arr[arr[i]] += 1

    # Find missing number
    for i in range(1, n + 1):
        if hash_arr[i] == 0:
            return i

    return -1


arr = [8, 2, 4, 5, 3, 7, 1]

print(missingNum(arr))
```

---

## Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(N) |

---

## Why We Should NOT Prefer This Approach

### 1. Extra Space Usage

We use an extra array of size `n`.

---

### 2. Not Space Efficient

For large `n`, memory usage increases.

---

### 3. Not Optimal

We can solve without extra space.

---

# 3. Optimal Approach 1 (Sum Formula)

## Key Idea

Sum of first `n` natural numbers:

```text
n * (n + 1) / 2
```

Missing number = expected sum − actual sum

---

## Algorithm

1. Compute expected sum of `[1..n]`
2. Compute actual sum of array
3. Subtract both

---

## Code

```python
def missingNum(arr):

    n = len(arr) + 1

    total_sum = sum(arr)

    expected_sum = n * (n + 1) // 2

    return expected_sum - total_sum


arr = [8, 2, 4, 5, 3, 7, 1]

print(missingNum(arr))
```

---

## Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(1) |

---

## Why This is Good

- No extra space
- Simple math
- Fast

---

## Limitation

- Risk of integer overflow in some languages
- Not safe for very large values

---

# 4. Optimal Approach 2 (XOR Method)

## Key Idea

Properties of XOR:

```text
x ^ x = 0
x ^ 0 = x
```

So:

```text
(1 ^ 2 ^ 3 ^ ... ^ n) ^ (array elements) = missing number
```

---

## Algorithm

1. XOR all numbers from `1 to n`
2. XOR all array elements
3. XOR both results

---

## Code

```python
def missingNum(arr):

    n = len(arr) + 1

    xor1 = 0
    xor2 = 0

    # XOR array elements
    for i in range(n - 1):
        xor2 ^= arr[i]

    # XOR numbers 1 to n
    for i in range(1, n + 1):
        xor1 ^= i

    return xor1 ^ xor2


arr = [8, 2, 4, 5, 3, 7, 1]

print(missingNum(arr))
```

---

## Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(1) |

---

# Why XOR Approach is Best

## 1. No Overflow Issues

Unlike sum formula.

---

## 2. No Extra Space

Constant space used.

---

## 3. Very Efficient

Fast bitwise operations.

---

## 4. Interview Favorite

Commonly asked in coding interviews.

---

# Final Comparison

| Approach | Time Complexity | Space Complexity | Notes |
|---|---|---|---|
| Brute Force | O(N²) | O(1) | Slow |
| Hashing | O(N) | O(N) | Extra space |
| Sum Formula | O(N) | O(1) | Overflow risk |
| XOR (Best) | O(N) | O(1) | Most optimal |

---

# Interview Tips

## When explaining this problem:

Start like this:

1. Brute force (for intuition)
2. Hashing (for improvement)
3. Sum formula (math optimization)
4. XOR (best optimal solution)

---

# Key Learning

For problems like “missing number”:

- Look for mathematical patterns
- Try sum or XOR tricks
- Avoid nested loops
- Optimize space whenever possible

This is one of the most important “pattern recognition” problems in arrays.
