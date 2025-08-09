# Trapping Rain Water - Java Solution

## Problem
You are given an array `height[]` where each element represents the height of a bar.  
We need to find how much water can be trapped after raining.

**Example:**
Explanation:  
Total trapped water = 9 units.

---
<img width="1393" height="669" alt="image" src="https://github.com/user-attachments/assets/c5937df7-b1df-4427-a1d8-d3ae9d6ff5f5" />

## Approach
We solve this problem using **Prefix Max** and **Suffix Max** arrays.

1. **Prefix Max**:  
   For each index `i`, store the highest bar height from the left side up to `i`.

2. **Suffix Max**:  
   For each index `i`, store the highest bar height from the right side up to `i`.

3. **Water at each position**:  
   Water trapped at `i` = `min(PrefixMax[i], SuffixMax[i]) - height[i]`.

4. **Sum up** water trapped at each position to get the final answer.

---

## Complexity
- **Time Complexity**: `O(n)` — We traverse the array three times.
- **Space Complexity**: `O(n)` — We use two arrays for prefix and suffix maximums.

---

## Java Code
```java
class Solution {
    public int trap(int[] height) {
        int[] prefixMax = new int[height.length];
        int[] suffixMax = new int[height.length];

        // Build prefix max
        int max = height[0];
        for (int i = 0; i < height.length; i++) {
            prefixMax[i] = Math.max(max, height[i]);
            max = prefixMax[i];
        }

        // Build suffix max
        max = height[height.length - 1];
        for (int j = height.length - 1; j >= 0; j--) {
            suffixMax[j] = Math.max(max, height[j]);
            max = suffixMax[j];
        }

        // Calculate trapped water
        int total_trap = 0;
        for (int i = 0; i < height.length; i++) {
            total_trap += Math.min(prefixMax[i], suffixMax[i]) - height[i];
        }

        return total_trap;
    }
}
