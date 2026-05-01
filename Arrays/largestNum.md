# Python and Java: Finding the Maximum Value

Python is concise. A senior developer would typically use the built-in `max()` function but understands how the manual loop works for custom objects or logic.

## Python Implementation (`max_finder.py`)
```python
def get_max(arr):
    if not arr:
        return None
    
    # 1. Standard Built-in (Highly Optimized)
    # return max(arr)

    # 2. Algorithmic Approach (O(n))
    max_val = arr[0]
    for num in arr:
        if num > max_val:
            max_val = num
    return max_val

# Test
data = [42, 7, 103, 15, 88]
print(f"The largest number is: {get_max(data)}")
```

## Use Code with Caution in Java Implementation
Java requires more boilerplate. A senior developer uses Streams for readability or Loops for raw performance.

```java
// MaxFinder.java
import java.util.Arrays;

public class MaxFinder {
    public static void main(String[] args) {
        int[] data = {42, 7, 103, 15, 88};

        try {
            System.out.println("Largest (Stream): " + findMaxStream(data));
            System.out.println("Largest (Loop): " + findMaxLoop(data));
        } catch (Exception e) {
            System.err.println(e.getMessage());
        }
    }

    // Modern Java 8+ Approach
    public static int findMaxStream(int[] arr) {
        return Arrays.stream(arr)
                     .max()
                     .orElseThrow(() -> new RuntimeException("Array is empty"));
    }

    // Classic High-Performance Approach
    public static int findMaxLoop(int[] arr) {
        if (arr == null || arr.length == 0) {
            throw new IllegalArgumentException("Array cannot be empty");
        }
        int max = arr[0];
        for (int num : arr) {
            if (num > max) max = num;
        }
        return max;
}
