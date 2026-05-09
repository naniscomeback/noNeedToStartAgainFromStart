# Second Smallest and Second Largest Element in an Array

## Problem Statement
Given an array, find the **second smallest** and **second largest** elements.

### Example

```python
Input:  [1, 2, 4, 6, 7, 5]

Output:
Second smallest = 2
Second largest = 6
```

---

# 1. Brute Force Approach

## Algorithm
1. Sort the array in ascending order.
2. The second element (`arr[1]`) will be the second smallest.
3. The second last element (`arr[n-2]`) will be the second largest.

---

## Code

```python
# Function to find the second smallest and second largest elements
def getElements(arr, n):

    # Edge case
    if n < 2:
        print(-1, -1)
        return

    # Sorting the array
    arr.sort()

    # Second smallest
    small = arr[1]

    # Second largest
    large = arr[n - 2]

    print("Second smallest is", small)
    print("Second largest is", large)


# Driver code
arr = [1, 2, 4, 6, 7, 5]
n = len(arr)

getElements(arr, n)
```

---

# Why We Should NOT Prefer This Approach

## 1. Sorting is Expensive

Sorting takes:

```text
Time Complexity = O(N log N)
```

But this problem can be solved in:

```text
O(N)
```

So sorting introduces unnecessary overhead.

---

## 2. Modifies the Original Array

`arr.sort()` changes the original input array.

### Example

```python
arr = [4, 2, 1]

arr.sort()

print(arr)
```

### Output

```python
[1, 2, 4]
```

If another part of the program depends on the original order, this may create bugs.

---

## 3. Fails for Duplicate Values

### Example

```python
arr = [1, 1, 2, 3]
```

After sorting:

```python
[1, 1, 2, 3]
```

`arr[1] = 1`

But `1` is NOT the second smallest distinct element.

Correct answer should be:

```python
2
```

---

# When We Can Use Brute Force

We can use this approach when:

- Input size is small
- Simplicity is more important than optimization
- Duplicates are not present
- The array is already sorted
- Performance is not critical

---

# Time and Space Complexity

| Complexity | Value |
|---|---|
| Time Complexity | O(N log N) |
| Space Complexity | O(1) |

---

# 2. Better Approach (Two Traversals)

## Algorithm

1. Find the smallest and largest elements.
2. Traverse the array again:
   - Find the element just greater than the smallest
   - Find the element just smaller than the largest

---

## Code

```python
# Function to find the second smallest and second largest elements
def getElements(arr, n):

    # Edge case
    if n < 2:
        print(-1, -1)
        return

    # Initialize variables
    small = float('inf')
    second_small = float('inf')

    large = float('-inf')
    second_large = float('-inf')

    # First traversal
    for num in arr:
        small = min(small, num)
        large = max(large, num)

    # Second traversal
    for num in arr:

        if num < second_small and num != small:
            second_small = num

        if num > second_large and num != large:
            second_large = num

    print("Second smallest is", second_small)
    print("Second largest is", second_large)


# Driver code
arr = [1, 2, 4, 6, 7, 5]
n = len(arr)

getElements(arr, n)
```

---

# Advantages Over Brute Force

## 1. Better Time Complexity

```text
O(N) + O(N) = O(2N)
```

Ignoring constants:

```text
O(N)
```

Better than:

```text
O(N log N)
```

---

## 2. Original Array Remains Unchanged

No sorting is performed.

---

## 3. Handles Duplicate Values Properly

### Example

```python
arr = [1, 1, 2, 3]
```

### Output

```python
Second smallest = 2
```

Correct result.

---

# Drawback of This Approach

- Requires two traversals
- Can still be optimized further

---

# When We Can Use This Approach

- When better performance is needed
- When the original array should not be modified
- When duplicates exist
- Medium to large input sizes

---

# Time and Space Complexity

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(1) |

---

# 3. Optimal Approach (Single Traversal)

## Idea

Maintain:
- smallest
- second smallest
- largest
- second largest

in a single traversal.

---

## Code

```python
# Function to find second smallest element
def secondSmallest(arr):

    small = float('inf')
    second_small = float('inf')

    for num in arr:

        if num < small:
            second_small = small
            small = num

        elif num < second_small and num != small:
            second_small = num

    return second_small


# Function to find second largest element
def secondLargest(arr):

    large = float('-inf')
    second_large = float('-inf')

    for num in arr:

        if num > large:
            second_large = large
            large = num

        elif num > second_large and num != large:
            second_large = num

    return second_large


# Driver code
arr = [1, 2, 4, 7, 7, 5]

print("Second smallest is", secondSmallest(arr))
print("Second largest is", secondLargest(arr))
```

---

# Why This is the Best Solution

## 1. Single Traversal

Only one pass through the array.

---

## 2. Best Time Complexity

```text
O(N)
```

---

## 3. No Sorting Needed

Original array remains unchanged.

---

## 4. Handles Duplicates Correctly

### Example

```python
[1, 1, 2, 3]
```

Second smallest:

```python
2
```

Correct answer.

---

# When We Should Use This Approach

- Coding interviews
- Competitive programming
- Large datasets
- Performance-critical systems
- Real-world backend applications

---

# Time and Space Complexity

| Complexity | Value |
|---|---|
| Time Complexity | O(N) |
| Space Complexity | O(1) |

---

# Final Comparison

| Approach | Time Complexity | Modifies Array | Handles Duplicates | Traversals |
|---|---|---|---|---|
| Brute Force (Sorting) | O(N log N) | Yes | No | 1 |
| Better Approach | O(N) | No | Yes | 2 |
| Optimal Approach | O(N) | No | Yes | 1 |

---

# Interview Discussion Points

## Why Brute Force is Not Preferred
- Sorting increases complexity
- Modifies original array
- Duplicate handling issue

---

## Why Optimal Approach is Better
- Single traversal
- O(N) complexity
- Space efficient
- Cleaner logic
- Better scalability

---

# Key Learning

Always ask:
1. Can we avoid sorting?
2. Can we reduce traversals?
3. Can we optimize time complexity?
4. Are duplicates handled properly?
5. Does the solution modify input data?

These are the points interviewers usually look for.
