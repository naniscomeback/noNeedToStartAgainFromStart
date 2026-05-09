# Left Rotate the Array by One

## Problem Statement

Given an integer array `nums`, rotate the array to the left by one position.

### Note
- Do not return anything
- Modify the array in-place

---

# Examples

## Example 1

```python
Input:  [1, 2, 3, 4, 5]

Output: [2, 3, 4, 5, 1]
```

---

## Example 2

```python
Input:  [10, 20, 30]

Output: [20, 30, 10]
```

---

# 1. Brute Force Approach

## Algorithm

1. Create a temporary array of the same size
2. Shift all elements one position to the left
3. Place the first element at the last position
4. Copy/print the temporary array

---

## Code

```python
# Function to rotate array left by one position
def solve(arr, n):

    # Temporary array
    temp = [0] * n

    # Shift elements
    for i in range(1, n):
        temp[i - 1] = arr[i]

    # First element goes to last
    temp[n - 1] = arr[0]

    # Print rotated array
    for num in temp:
        print(num, end=" ")

    print()


# Driver code
if __name__ == "__main__":

    arr = [1, 2, 3, 4, 5]
    n = len(arr)

    solve(arr, n)
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(N) |

---

# Why We Should NOT Prefer This Approach

## 1. Extra Space Usage

A temporary array is created.

```python
temp = [0] * n
```

This increases memory usage.

---

## 2. Not In-Place

The problem statement usually expects:

```text
Modify the original array directly
```

But this approach uses another array.

---

## 3. Unnecessary Memory Overhead

For very large arrays:

```python
N = 1000000
```

Extra memory allocation becomes costly.

---

## 4. Less Efficient

Even though time complexity is good:

```text
O(N)
```

space optimization is poor.

---

# When We Can Use Brute Force

This approach is acceptable when:

- Simplicity is preferred
- Space optimization is not important
- Input size is small
- Learning basic array manipulation

---

# 2. Optimal Approach (In-Place Rotation)

## Algorithm

1. Store the first element in a temporary variable
2. Shift all elements one step left
3. Place stored element at the last index

---

## Code

```python
class Solution:

    def rotateArrayByOne(self, nums):

        # Store first element
        temp = nums[0]

        # Shift elements left
        for i in range(1, len(nums)):
            nums[i - 1] = nums[i]

        # Place first element at end
        nums[-1] = temp


# Driver code
if __name__ == "__main__":

    nums = [1, 2, 3, 4, 5]

    solution = Solution()

    solution.rotateArrayByOne(nums)

    print(nums)
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(1) |

---

# Why This is the Best Solution

## 1. In-Place Modification

No extra array is used.

The original array is modified directly.

---

## 2. Constant Space Complexity

```text
O(1)
```

Very memory efficient.

---

## 3. Single Traversal

The array is traversed only once.

---

## 4. Efficient for Large Inputs

Works efficiently even for large datasets.

---

# Dry Run

## Input

```python
[1, 2, 3, 4, 5]
```

---

## Step 1

Store first element:

```python
temp = 1
```

---

## Step 2

Shift elements left:

| Index | Array State |
|---|---|
| i = 1 | [2, 2, 3, 4, 5] |
| i = 2 | [2, 3, 3, 4, 5] |
| i = 3 | [2, 3, 4, 4, 5] |
| i = 4 | [2, 3, 4, 5, 5] |

---

## Step 3

Place first element at end:

```python
[2, 3, 4, 5, 1]
```

---

# When We Should Use This Approach

- Coding interviews
- Competitive programming
- Memory-constrained systems
- Large arrays
- Real-world applications

---

# Final Comparison

| Approach | Time Complexity | Space Complexity | In-Place | Efficient |
|---|---|---|---|---|
| Brute Force | O(N) | O(N) | No | Moderate |
| Optimal Approach | O(N) | O(1) | Yes | Best |

---

# Interview Discussion Points

## Why Brute Force is Not Preferred

- Uses extra memory
- Not in-place
- Less optimized

---

## Why Optimal Approach is Better

- Constant space
- In-place modification
- Cleaner logic
- Better memory efficiency

---

# Key Learning

Whenever working with array rotation problems:

1. Think about in-place modification
2. Avoid unnecessary extra arrays
3. Optimize space complexity
4. Use temporary variables wisely

Array rotation problems are very common in coding interviews.
