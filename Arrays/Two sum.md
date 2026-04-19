import os

"""# Two Sum: Hash Map Optimization

This repository demonstrates the optimal solution for the classic **Two Sum** problem using Hash Maps in both Python and Java.

## The Problem
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`.

- **Constraint:** We must find a solution better than $O(n^2)$ (nested loops).
- **Optimization:** We use a **Hash Map** to store visited numbers, allowing for $O(1)$ lookups.

---

## 1. Python Implementation
Python's `dict` is an implementation of a hash map. It allows us to check for the "missing piece" (target - current) in constant time.

```python
class Solution(object):
    def twoSum(self, nums, target):
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        # s is our Hash Map (Dictionary)
        s = {} 
        
        for i in range(0, len(nums)):
            # Calculate the "Missing Piece"
            complement = target - nums[i]
            
            # Check if we have seen the missing piece before
            if complement in s:
                # Return the index of the complement and the current index
                return [s[complement], i]
            else:
                # Store the current number as the key and its index as the value
                s[nums[i]] = i
```
**using java**

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        // Create a Map: Key is the number, Value is its index
        Map<Integer, Integer> s = new HashMap<>();
        
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            
            // containsKey() is the Java equivalent of "in" in Python
            if (s.containsKey(complement)) {
                return new int[] { s.get(complement), i };
            }
            
            // put() adds the entry to the Map
            s.put(nums[i], i);
        }
        
        // Return an empty array if no solution is found
        return new int[] {};
    }
}
