# Rotate Array by K Elements

## Problem Statement

Given an array of integers, rotate the array by `k` positions either:

- Left rotation
- Right rotation

---

# Examples

## Example 1 — Right Rotation

```python
Input:
arr = [1, 2, 3, 4, 5, 6, 7]
k = 2

Output:
[6, 7, 1, 2, 3, 4, 5]
```

---

## Example 2 — Left Rotation

```python
Input:
arr = [1, 2, 3, 4, 5, 6, 7]
k = 2

Output:
[3, 4, 5, 6, 7, 1, 2]
```

---

# 1. Brute Force Approach

## Idea

Use a temporary array to store elements that will be rotated.

---

# Right Rotation by K

## Algorithm

1. Store last `k` elements in a temporary array
2. Shift remaining `n-k` elements right by `k` positions
3. Copy stored elements to the beginning

---

# Left Rotation by K

## Algorithm

1. Store first `k` elements in a temporary array
2. Shift remaining elements left by `k` positions
3. Copy stored elements to the end

---

# Code

```python
class Solution:

    # Rotate array right by k positions
    def rotateRight(self, arr, k):

        n = len(arr)

        if n == 0:
            return

        # Normalize k
        k %= n

        # Store last k elements
        temp = arr[-k:]

        # Shift remaining elements
        for i in range(n - k - 1, -1, -1):
            arr[i + k] = arr[i]

        # Copy temp to front
        for i in range(k):
            arr[i] = temp[i]

    # Rotate array left by k positions
    def rotateLeft(self, arr, k):

        n = len(arr)

        if n == 0:
            return

        # Normalize k
        k %= n

        # Store first k elements
        temp = arr[:k]

        # Shift remaining elements
        for i in range(k, n):
            arr[i - k] = arr[i]

        # Copy temp to end
        for i in range(k):
            arr[n - k + i] = temp[i]


# Driver code
sol = Solution()

arr = [1, 2, 3, 4, 5, 6, 7]

k = 2

sol.rotateRight(arr, k)

print("Right Rotation:", arr)

arr2 = [1, 2, 3, 4, 5, 6, 7]

sol.rotateLeft(arr2, k)

print("Left Rotation:", arr2)
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(K) |

---

# Why We Should NOT Prefer This Approach

## 1. Extra Space Usage

Temporary arrays are used:

```python
temp = arr[-k:]
```

or

```python
temp = arr[:k]
```

This increases memory usage.

---

## 2. Not Fully In-Place

The problem can be solved without extra arrays.

---

## 3. Less Memory Efficient

For very large arrays and large `k`:

```python
N = 10^6
```

extra memory becomes expensive.

---

## 4. Multiple Data Movements

Elements are copied multiple times.

This slightly increases overhead.

---

# When We Can Use Brute Force

This approach is acceptable when:

- Simplicity is preferred
- Space optimization is not important
- Input size is small
- Quick implementation is needed

---

# 2. Optimal Approach (Reversal Algorithm)

## Key Idea

Rotation can be achieved using array reversals.

Instead of moving elements one by one:

```text
Reverse sections of the array
```

This allows:

- In-place rotation
- Constant extra space

---

# Right Rotation by K

## Steps

1. Reverse entire array
2. Reverse first `k` elements
3. Reverse remaining `n-k` elements

---

# Example

## Input

```python
[1, 2, 3, 4, 5, 6, 7]
k = 2
```

---

## Step 1 — Reverse Entire Array

```python
[7, 6, 5, 4, 3, 2, 1]
```

---

## Step 2 — Reverse First K Elements

```python
[6, 7, 5, 4, 3, 2, 1]
```

---

## Step 3 — Reverse Remaining Elements

```python
[6, 7, 1, 2, 3, 4, 5]
```

Final Answer.

---

# Left Rotation by K

## Steps

1. Reverse first `k` elements
2. Reverse remaining `n-k` elements
3. Reverse entire array

---

# Code

```python
class Solution:

    # Helper function to reverse array
    def reverse(self, nums, start, end):

        while start < end:

            nums[start], nums[end] = nums[end], nums[start]

            start += 1
            end -= 1

    # Rotate array
    def rotateArray(self, nums, k, direction):

        n = len(nums)

        # Edge cases
        if n == 0 or k == 0:
            return nums

        # Normalize k
        k = k % n

        # Right rotation
        if direction == "right":

            # Reverse entire array
            self.reverse(nums, 0, n - 1)

            # Reverse first k elements
            self.reverse(nums, 0, k - 1)

            # Reverse remaining elements
            self.reverse(nums, k, n - 1)

        # Left rotation
        elif direction == "left":

            # Reverse first k elements
            self.reverse(nums, 0, k - 1)

            # Reverse remaining elements
            self.reverse(nums, k, n - 1)

            # Reverse entire array
            self.reverse(nums, 0, n - 1)

        return nums


# Driver code
sol = Solution()

nums = [1, 2, 3, 4, 5, 6, 7]

k = 2

direction = "right"

result = sol.rotateArray(nums, k, direction)

print(result)
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(1) |

---

# Why This is the Best Solution

## 1. In-Place Rotation

No temporary array is used.

---

## 2. Constant Space Complexity

```text
O(1)
```

Very memory efficient.

---

## 3. Efficient for Large Inputs

Works efficiently for large datasets.

---

## 4. Standard Interview Solution

The reversal algorithm is the expected optimized approach in interviews.

---

## 5. Cleaner Rotation Logic

Rotation becomes easier using reversals.

---

# Important Observation

## Why We Use

```python
k = k % n
```

Example:

```python
n = 7
k = 9
```

Rotating 9 times is same as rotating:

```python
9 % 7 = 2
```

This avoids unnecessary operations.

---

# When We Should Use This Approach

- Coding interviews
- Competitive programming
- Large arrays
- Memory-constrained systems
- Performance-critical applications

---

# Final Comparison

| Approach | Time Complexity | Space Complexity | In-Place | Efficient |
|---|---|---|---|---|
| Brute Force | O(N) | O(K) | No | Moderate |
| Optimal (Reversal Algorithm) | O(N) | O(1) | Yes | Best |

---

# Interview Discussion Points

## Why Brute Force is Not Preferred

- Uses extra memory
- Multiple data movements
- Less optimized

---

## Why Optimal Approach is Better

- In-place modification
- Constant extra space
- Efficient reversal logic
- Better scalability

---

# Key Learning

Whenever solving array rotation problems:

1. Think about reversal techniques
2. Optimize space complexity
3. Use modulo operation for large k
4. Avoid unnecessary extra arrays

The reversal algorithm is one of the most important array interview patterns.
