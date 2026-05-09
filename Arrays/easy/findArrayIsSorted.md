# Check if an Array is Sorted

## Problem Statement

Given an array of size `N`, write a program to check whether the array is sorted in:

- Ascending order
- Increasing order
- Non-decreasing order

If the array is sorted, return `True`; otherwise, return `False`.

---

# Example

```python
Input:  [1, 2, 3, 4, 5]
Output: True
```

```python
Input:  [1, 3, 2, 4, 5]
Output: False
```

---

# 1. Brute Force Approach

## Algorithm

1. Start from index `0`.
2. Compare the current element with all future elements.
3. If any future element is smaller than the current element:
   - The array is not sorted.
   - Return `False`.
4. If the entire array is traversed successfully:
   - Return `True`.

---

## Code

```python
# Function to check if the array is sorted
def isSorted(arr, n):

    for i in range(n):

        for j in range(i + 1, n):

            # If any future element is smaller
            if arr[j] < arr[i]:
                return False

    return True


# Driver code
arr = [1, 2, 3, 4, 5]
n = len(arr)

ans = isSorted(arr, n)

print("True" if ans else "False")
```

---

# Why We Should NOT Prefer This Approach

## 1. Unnecessary Comparisons

For every element, we compare with all future elements.

Example:

```python
[1, 2, 3, 4, 5]
```

Even though the array is already sorted, many extra comparisons are performed.

---

## 2. High Time Complexity

Nested loops are used.

### Time Complexity

```text
O(N²)
```

This becomes inefficient for large arrays.

---

## 3. Poor Scalability

For large datasets:

```python
N = 100000
```

The number of comparisons becomes huge.

This can lead to performance issues in interviews and real-world systems.

---

# When We Can Use Brute Force

We can use this approach when:

- Input size is very small
- Simplicity is preferred
- Performance is not important
- Educational purposes (understanding logic)

---

# Time and Space Complexity

| Complexity | Value |
|---|---|
| Time Complexity | O(N²) |
| Space Complexity | O(1) |

---

# 2. Optimal Approach

## Key Observation

In a sorted array:

```text
Previous element <= Current element
```

If this condition is true for every element, then the array is sorted.

---

## Algorithm

1. Start from index `1`.
2. Compare every element with its previous element.
3. If:

```python
arr[i] < arr[i - 1]
```

then the array is not sorted.

4. Otherwise continue traversal.
5. If traversal completes successfully:
   - Return `True`.

---

## Code

```python
# Function to check if the array is sorted
def isSorted(arr, n):

    for i in range(1, n):

        # If current element is smaller than previous
        if arr[i] < arr[i - 1]:
            return False

    return True


# Driver code
arr = [1, 2, 3, 4, 5]
n = len(arr)

print("True" if isSorted(arr, n) else "False")
```

---

# Why This is the Best Solution

## 1. Single Traversal

The array is traversed only once.

---

## 2. Better Time Complexity

```text
O(N)
```

Much better than:

```text
O(N²)
```

---

## 3. Early Exit Optimization

If an unsorted pair is found early:

```python
[1, 5, 2, 3, 4]
```

The algorithm immediately returns `False`.

No unnecessary comparisons are performed.

---

## 4. Space Efficient

No extra space is used.

---

# When We Should Use This Approach

- Coding interviews
- Competitive programming
- Large datasets
- Real-world applications
- Performance-critical systems

---

# Time and Space Complexity

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(1) |

---

# Final Comparison

| Approach | Time Complexity | Traversals | Efficient for Large Inputs |
|---|---|---|---|
| Brute Force | O(N²) | Multiple | No |
| Optimal Approach | O(N) | Single | Yes |

---

# Interview Discussion Points

## Why Brute Force is Not Preferred

- Too many unnecessary comparisons
- Uses nested loops
- Poor performance for large arrays

---

## Why Optimal Approach is Better

- Single traversal
- Faster execution
- Early exit optimization
- Cleaner and simpler logic
- Better scalability

---

# Key Learning

Whenever checking if an array is sorted:

1. Compare adjacent elements only
2. Avoid unnecessary nested loops
3. Think about early exit conditions
4. Optimize time complexity whenever possible

These optimization discussions are important in coding interviews.
