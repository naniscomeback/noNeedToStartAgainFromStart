# Move All Zeros to the End of the Array

## Problem Statement

Given an integer array, move all zeros to the end of the array while maintaining the relative order of non-zero elements.

### Note
- Modify the array in-place if possible
- Maintain the original order of non-zero elements

---

# Examples

## Example 1

```python
Input:  [0, 1, 0, 3, 12]

Output: [1, 3, 12, 0, 0]
```

---

## Example 2

```python
Input:  [1, 2, 0, 4, 0, 5]

Output: [1, 2, 4, 5, 0, 0]
```

---

## Example 3

```python
Input:  [0, 0, 0]

Output: [0, 0, 0]
```

---

# 1. Brute Force Approach

## Idea

Use an extra array to store all non-zero elements first.

Then fill remaining positions with zeros.

---

# Algorithm

1. Create a temporary array
2. Copy all non-zero elements into it
3. Fill remaining positions with zeros
4. Copy back to original array

---

# Code

```python
# Solution class
class Solution:

    # Function to move all zeroes to end
    def moveZeroes(self, arr):

        # Temporary array
        temp = [0] * len(arr)

        # Pointer for temp array
        index = 0

        # Copy non-zero elements
        for num in arr:

            if num != 0:

                temp[index] = num

                index += 1

        # Copy temp back to original array
        for i in range(len(arr)):

            arr[i] = temp[i]

        return arr


# Driver code
arr = [0, 1, 0, 3, 12]

sol = Solution()

result = sol.moveZeroes(arr)

print(result)
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

A temporary array is created:

```python
temp = [0] * len(arr)
```

This increases memory usage.

---

## 2. Not Fully In-Place

The problem can be solved without extra arrays.

---

## 3. Additional Copying Operations

Elements are copied multiple times:

- Original → temp
- Temp → original

This increases overhead.

---

## 4. Less Efficient for Large Inputs

For large arrays:

```python
N = 10^6
```

extra memory becomes costly.

---

# When We Can Use Brute Force

This approach is acceptable when:

- Simplicity is preferred
- Space optimization is not important
- Input size is small
- Learning array manipulation

---

# 2. Optimal Approach (Two Pointers)

## Key Idea

Use two pointers:

- `j` → points to first zero
- `i` → traverses the array

Whenever a non-zero element is found:

```python
Swap nums[i] with nums[j]
```

This moves non-zero elements forward while pushing zeros backward.

---

# Algorithm

1. Find the first zero index using pointer `j`
2. Traverse remaining array using pointer `i`
3. If `nums[i]` is non-zero:
   - Swap `nums[i]` and `nums[j]`
   - Increment `j`

---

# Code

```python
class Solution:

    # Function to move zeroes to end
    def moveZeroes(self, nums):

        # Pointer to first zero
        j = -1

        # Find first zero
        for i in range(len(nums)):

            if nums[i] == 0:

                j = i
                break

        # No zero found
        if j == -1:
            return

        # Traverse remaining array
        for i in range(j + 1, len(nums)):

            # Found non-zero element
            if nums[i] != 0:

                # Swap
                nums[i], nums[j] = nums[j], nums[i]

                # Move j forward
                j += 1


# Driver code
nums = [0, 1, 0, 3, 12]

sol = Solution()

sol.moveZeroes(nums)

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

---

## 2. Constant Space Complexity

```text
O(1)
```

Very memory efficient.

---

## 3. Single Traversal

The array is traversed only once after locating the first zero.

---

## 4. Maintains Relative Order

Non-zero elements maintain their original order.

---

## 5. Efficient for Large Inputs

Works efficiently for large datasets.

---

# Dry Run

## Input

```python
[0, 1, 0, 3, 12]
```

---

## Step 1

Find first zero:

```python
j = 0
```

---

## Step 2

Traverse using `i`

| i | nums[i] | Action | Array |
|---|---|---|---|
| 1 | 1 | Swap with nums[0] | [1,0,0,3,12] |
| 2 | 0 | Ignore | [1,0,0,3,12] |
| 3 | 3 | Swap with nums[1] | [1,3,0,0,12] |
| 4 | 12 | Swap with nums[2] | [1,3,12,0,0] |

---

# Final Output

```python
[1, 3, 12, 0, 0]
```

---

# When We Should Use This Approach

- Coding interviews
- Competitive programming
- Large datasets
- Memory-constrained systems
- Backend systems

---

# Final Comparison

| Approach | Time Complexity | Space Complexity | In-Place | Efficient |
|---|---|---|---|---|
| Brute Force | O(N) | O(N) | No | Moderate |
| Optimal (Two Pointers) | O(N) | O(1) | Yes | Best |

---

# Interview Discussion Points

## Why Brute Force is Not Preferred

- Uses extra memory
- Multiple copying operations
- Less optimized

---

## Why Optimal Approach is Better

- Constant space
- In-place modification
- Maintains order
- Better scalability

---

# Key Learning

Whenever solving array rearrangement problems:

1. Think about two-pointer techniques
2. Avoid unnecessary extra arrays
3. Optimize space complexity
4. Maintain relative ordering carefully

Two-pointer strategy is one of the most important interview patterns for arrays.
