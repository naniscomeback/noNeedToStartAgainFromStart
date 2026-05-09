# Remove Duplicates In-Place from Sorted Array

## Problem Statement

Given an integer array sorted in non-decreasing order, remove duplicates in-place such that each unique element appears only once.

The relative order of elements should remain the same.

After removing duplicates:

- The first `k` elements should contain the unique elements
- Return `k`
- Elements beyond `k` do not matter

---

# Examples

## Example 1

```python
Input:  [0,0,1,1,1,2,2,3,3,4]

Output:
k = 5
nums = [0,1,2,3,4]
```

---

## Example 2

```python
Input:  [1,1,2]

Output:
k = 2
nums = [1,2]
```

---

# 1. Brute Force Approach (Using Set)

## Algorithm

1. Create a `set` to store unique elements
2. Traverse the array
3. Insert elements into the set
4. Traverse the set and overwrite the original array
5. Return the number of unique elements

---

## Code

```python
# Solution class containing removeDuplicates method
class Solution:

    # Removes duplicates using set
    def removeDuplicates(self, nums):

        # Set to store unique values
        seen = set()

        # Position to insert unique values
        index = 0

        # Traverse array
        for num in nums:

            # If unique
            if num not in seen:

                # Add to set
                seen.add(num)

                # Place unique element
                nums[index] = num

                # Move index
                index += 1

        return index


# Driver code
nums = [0,0,1,1,1,2,2,3,3,4]

sol = Solution()

k = sol.removeDuplicates(nums)

print("k =", k)
print("Array after removing duplicates:", nums[:k])
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

A set is used to store unique elements.

This violates the in-place constraint of the problem.

---

## 2. Additional Memory Overhead

For large arrays:

```python
N = 1000000
```

The set may consume significant extra memory.

---

## 3. Unnecessary Data Structure

Since the array is already sorted:

```python
Duplicate elements are adjacent
```

Using a set becomes unnecessary.

---

## 4. Not Truly In-Place

Interviewers usually expect:

```text
O(1) extra space
```

But this approach uses:

```text
O(N) space
```

---

# When We Can Use This Approach

This approach is acceptable when:

- Space optimization is not important
- Simplicity is preferred
- Input size is small
- Quick implementation is needed

---

# 2. Optimal Approach (Two Pointers)

## Key Observation

Since the array is sorted:

```text
Duplicate elements appear next to each other
```

We can use two pointers:

- `i` → tracks last unique element
- `j` → traverses the array

---

# Algorithm

1. Keep first element as unique
2. Traverse array from second element
3. Compare current element with last unique element
4. If different:
   - Move unique pointer forward
   - Place current element there
5. Continue until traversal completes
6. Return count of unique elements

---

# Code

```python
# Class containing solution
class Solution:

    # Remove duplicates in-place
    def removeDuplicates(self, nums):

        # Edge case
        if not nums:
            return 0

        # Pointer for unique elements
        i = 0

        # Traverse array
        for j in range(1, len(nums)):

            # Found new unique element
            if nums[j] != nums[i]:

                # Move unique pointer
                i += 1

                # Place unique element
                nums[i] = nums[j]

        # Total unique elements
        return i + 1


# Driver code
nums = [0,0,1,1,1,2,2,3,3,4]

sol = Solution()

k = sol.removeDuplicates(nums)

print("Unique count =", k)
print("Array after removing duplicates:", nums[:k])
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

No extra data structure is used.

---

## 2. Constant Space Complexity

```text
O(1)
```

This satisfies interview requirements.

---

## 3. Single Traversal

The array is traversed only once.

---

## 4. Efficient for Large Inputs

Works efficiently even for very large arrays.

---

## 5. Maintains Relative Order

The original order of unique elements is preserved.

---

# Dry Run

## Input

```python
[0,0,1,1,1,2,2,3,3,4]
```

---

## Step-by-Step

| j | nums[j] | nums[i] | Action | Array |
|---|---|---|---|---|
| 1 | 0 | 0 | Skip duplicate | [0,0,1,1,1,2,2,3,3,4] |
| 2 | 1 | 0 | Place unique | [0,1,1,1,1,2,2,3,3,4] |
| 3 | 1 | 1 | Skip duplicate | |
| 4 | 1 | 1 | Skip duplicate | |
| 5 | 2 | 1 | Place unique | [0,1,2,1,1,2,2,3,3,4] |
| 6 | 2 | 2 | Skip duplicate | |
| 7 | 3 | 2 | Place unique | [0,1,2,3,1,2,2,3,3,4] |
| 8 | 3 | 3 | Skip duplicate | |
| 9 | 4 | 3 | Place unique | [0,1,2,3,4,2,2,3,3,4] |

---

## Final Output

```python
k = 5
nums = [0,1,2,3,4]
```

---

# When We Should Use This Approach

- Coding interviews
- Competitive programming
- Memory-constrained systems
- Large datasets
- Real-world backend applications

---

# Final Comparison

| Approach | Time Complexity | Space Complexity | In-Place | Efficient |
|---|---|---|---|---|
| Brute Force (Set) | O(N) | O(N) | No | Moderate |
| Optimal (Two Pointers) | O(N) | O(1) | Yes | Best |

---

# Interview Discussion Points

## Why Brute Force is Not Preferred

- Uses extra memory
- Violates in-place requirement
- Unnecessary use of set
- Less optimized

---

## Why Optimal Approach is Better

- Uses constant space
- Single traversal
- Fully in-place
- Cleaner logic
- Better scalability

---

# Key Learning

Whenever dealing with sorted arrays:

1. Think about adjacent duplicates
2. Use two-pointer techniques
3. Avoid unnecessary extra space
4. Optimize both time and space complexity

Two-pointer strategy is one of the most important patterns in coding interviews.
