# Union of Two Sorted Arrays

## Problem Statement

Given two sorted arrays `arr1` and `arr2` of size `n` and `m`, find the union of the two arrays.

The union of two arrays contains:

- All distinct elements
- Common elements only once
- Elements in ascending order

---

# Examples

## Example 1

```python
Input:
arr1 = [1, 2, 3, 4, 5]
arr2 = [2, 3, 4, 4, 5, 6]

Output:
[1, 2, 3, 4, 5, 6]
```

---

## Example 2

```python
Input:
arr1 = [1, 1, 2, 3]
arr2 = [2, 2, 4]

Output:
[1, 2, 3, 4]
```

---

# 1. Approach Using Map (Dictionary)

## Idea

Use a map/dictionary to store frequencies of all elements from both arrays.

Since keys in a map are unique:

```text
Duplicate elements are automatically removed
```

---

# Why Not Use unordered_map?

In C++:

- `unordered_map` stores keys in random order
- `map` stores keys in sorted order

Since the problem requires:

```text
Ascending order
```

using `map` is preferable.

In Python:

```python
sorted(freq.keys())
```

is used to maintain sorted order.

---

# Algorithm

1. Create an empty dictionary `freq`
2. Traverse `arr1` and store frequencies
3. Traverse `arr2` and store frequencies
4. Extract unique keys
5. Sort keys
6. Return result

---

# Code

```python
# Solution class
class Solution:

    # Function to find union
    def FindUnion(self, arr1, arr2, n, m):

        # Dictionary to store frequency
        freq = {}

        # Traverse first array
        for i in range(n):

            freq[arr1[i]] = freq.get(arr1[i], 0) + 1

        # Traverse second array
        for i in range(m):

            freq[arr2[i]] = freq.get(arr2[i], 0) + 1

        # Sorted unique elements
        Union = sorted(freq.keys())

        return Union


# Driver code
arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

arr2 = [2, 3, 4, 4, 5, 11, 12]

obj = Solution()

result = obj.FindUnion(arr1, arr2, len(arr1), len(arr2))

print(result)
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O((N + M) log(N + M)) |
| Space Complexity | O(N + M) |

---

# Why We Should NOT Prefer This Approach

## 1. Extra Space Usage

A dictionary/map is used.

This increases memory usage.

---

## 2. Sorting Overhead

Even though arrays are already sorted:

```python
sorted(freq.keys())
```

is still needed.

This adds extra complexity.

---

## 3. Not Using Sorted Property Efficiently

The input arrays are already sorted.

This approach ignores that advantage.

---

## 4. Less Optimized for Interviews

Interviewers usually expect:

```text
Two Pointer Approach
```

for sorted arrays.

---

# When We Can Use This Approach

This approach is acceptable when:

- Simplicity is preferred
- Input arrays are unsorted
- Space optimization is not important
- Fast implementation is needed

---

# 2. Approach Using Set

## Idea

A set automatically stores only unique elements.

We can insert elements from both arrays into the set.

---

# Why Not unordered_set?

In C++:

- `unordered_set` stores elements randomly
- `set` stores elements in sorted order

Since sorted output is required:

```text
set is preferable
```

In Python:

```python
sorted(set)
```

is used.

---

# Algorithm

1. Create a set
2. Insert elements from `arr1`
3. Insert elements from `arr2`
4. Convert set into sorted list
5. Return result

---

# Code

```python
class Solution:

    # Function to find union using set
    def findUnion(self, arr1, arr2):

        # Union of sets
        st = set(arr1) | set(arr2)

        # Return sorted result
        return sorted(st)


# Driver code
arr1 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

arr2 = [2, 3, 4, 4, 5, 11, 12]

obj = Solution()

result = obj.findUnion(arr1, arr2)

print(result)
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N + M + K log K) |
| Space Complexity | O(N + M) |

Where:

```text
K = Number of unique elements
```

---

# Why We Should NOT Prefer This Approach

## 1. Extra Space Usage

Set stores all unique elements separately.

---

## 2. Sorting Required

Sets do not guarantee sorted order in Python.

So:

```python
sorted(st)
```

is required.

---

## 3. Ignores Sorted Nature of Arrays

The arrays are already sorted.

We should use that advantage.

---

# Better/Optimal Approach (Two Pointers)

> NOTE:
> Your provided content did not include the optimal approach,
> but in interviews, the expected solution is usually the Two Pointer Approach.

---

# Optimal Idea

Since both arrays are already sorted:

- Use two pointers
- Compare elements
- Add smaller element
- Skip duplicates

This avoids:

- Extra sorting
- Unnecessary hash structures

---

# Algorithm

1. Initialize pointers `i` and `j`
2. Compare `arr1[i]` and `arr2[j]`
3. Insert smaller element if not already added
4. Move corresponding pointer
5. If equal:
   - Add once
   - Move both pointers
6. Add remaining elements

---

# Code

```python
class Solution:

    def findUnion(self, arr1, arr2):

        i = 0
        j = 0

        union = []

        while i < len(arr1) and j < len(arr2):

            # Skip duplicates in union list
            if len(union) > 0:

                while i < len(arr1) and arr1[i] == union[-1]:
                    i += 1

                while j < len(arr2) and arr2[j] == union[-1]:
                    j += 1

                if i >= len(arr1) or j >= len(arr2):
                    break

            if arr1[i] < arr2[j]:

                union.append(arr1[i])
                i += 1

            elif arr1[i] > arr2[j]:

                union.append(arr2[j])
                j += 1

            else:

                union.append(arr1[i])

                i += 1
                j += 1

        # Remaining elements
        while i < len(arr1):

            if union[-1] != arr1[i]:
                union.append(arr1[i])

            i += 1

        while j < len(arr2):

            if union[-1] != arr2[j]:
                union.append(arr2[j])

            j += 1

        return union


# Driver code
arr1 = [1, 2, 3, 4, 5]

arr2 = [2, 3, 4, 5, 6]

obj = Solution()

print(obj.findUnion(arr1, arr2))
```

---

# Complexity Analysis

| Complexity | Value |
|---|---|
| Time Complexity | O(N + M) |
| Space Complexity | O(N + M) |

---

# Why This is the Best Solution

## 1. Uses Sorted Property Efficiently

No unnecessary sorting.

---

## 2. Linear Time Complexity

```text
O(N + M)
```

Very efficient.

---

## 3. No Hashing Overhead

No map/set required.

---

## 4. Standard Interview Solution

Two-pointer approach is the expected optimized solution.

---

# Final Comparison

| Approach | Time Complexity | Space Complexity | Uses Sorted Property | Efficient |
|---|---|---|---|---|
| Map | O((N+M) log(N+M)) | O(N+M) | No | Moderate |
| Set | O(N+M+KlogK) | O(N+M) | No | Moderate |
| Two Pointers | O(N+M) | O(N+M) | Yes | Best |

---

# Interview Discussion Points

## Why Map/Set Approaches are Not Preferred

- Extra memory usage
- Additional sorting required
- Ignores sorted nature of arrays

---

## Why Two Pointer Approach is Better

- Linear traversal
- Efficient merging
- Uses sorted property
- Cleaner interview solution

---

# Key Learning

Whenever arrays are sorted:

1. Think about two-pointer techniques
2. Avoid unnecessary hashing
3. Avoid extra sorting
4. Use linear traversal whenever possible

Two-pointer merging is one of the most important interview patterns for sorted arrays.
