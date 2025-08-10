```md
# Frog Jump Problem - Minimum Cost to Reach the End

## Problem Description
Given an array `height` where each element represents the height of a stone, a frog starts at the first stone and wants to reach the last stone. The frog can jump either:
1. 1 stone ahead (cost is absolute height difference)
2. Or 2 stones ahead (cost is absolute height difference)

We need to find the minimum total cost to reach the last stone.

## Solution Approaches

### 1. Brute Force Approach (Recursive)

```java
class Solution {
    public static int min = Integer.MAX_VALUE;
    
    public void solve(int[] nums, int n, int index, int cost) {
        if(index == n-1) {
            min = Math.min(min, cost);
            return;
        }
        if(index+1 < n) {
            int val = Math.abs(nums[index+1]-nums[index]);
            solve(nums, n, index+1, cost+val);
        }
        if(index+2 < n) {
            int val = Math.abs(nums[index+2]-nums[index]);
            solve(nums, n, index+2, cost+val);
        }
    }

    int minCost(int[] height) {
        min = Integer.MAX_VALUE;
        solve(height, height.length, 0, 0);
        return min;
    }
}
```

**Explanation:**
- This approach explores all possible paths recursively.
- At each stone, it tries both possible jumps (1 or 2 stones ahead).
- When it reaches the last stone, it updates the global minimum cost.
- **Time Complexity:** O(2^n) - Exponential time due to repeated calculations of same subproblems.
- **Space Complexity:** O(n) - Recursion stack space.

**Limitations:**
- Highly inefficient for larger inputs due to exponential time complexity.
- Recomputes the same subproblems multiple times.

### 2. Optimized Approach (Memoization - Top-down DP)

```java
class Solution {
    public int solve(int[] nums, int n, int index, int[] dp) {
        if(index == n-1) return 0;
        if(dp[index] != -1) return dp[index];

        int cost1 = Integer.MAX_VALUE;
        int cost2 = Integer.MAX_VALUE;

        if(index + 1 < n) {
            cost1 = Math.abs(nums[index+1] - nums[index]) 
                   + solve(nums, n, index+1, dp);
        }
        if(index + 2 < n) {
            cost2 = Math.abs(nums[index+2] - nums[index]) 
                   + solve(nums, n, index+2, dp);
        }

        return dp[index] = Math.min(cost1, cost2);
    }

    int minCost(int[] height) {
        int n = height.length;
        int[] dp = new int[n];
        java.util.Arrays.fill(dp, -1);
        return solve(height, n, 0, dp);
    }
}
```

**Explanation:**
- Uses memoization to store already computed results in a DP array.
- For each index, it checks if the result is already computed (stored in dp array).
- If not, computes the minimum cost from current index by considering both jumps.
- Stores the result in dp array before returning to avoid recomputation.
- **Time Complexity:** O(n) - Each index is computed only once.
- **Space Complexity:** O(n) - For the dp array and recursion stack.

**Advantages:**
- Dramatically reduces time complexity by avoiding recomputation.
- Much more efficient for larger inputs compared to brute force.

## Key Differences

| Aspect          | Brute Force | Optimized DP |
|-----------------|-------------|--------------|
| Time Complexity | O(2^n)      | O(n)         |
| Space Complexity| O(n)        | O(n)         |
| Approach        | Recursive   | Memoization  |
| Efficiency      | Low         | High         |
| Suitable for    | Small n     | Large n      |

The optimized DP approach is clearly superior for this problem as it efficiently solves it in linear time while the brute force approach becomes impractical even for moderately sized inputs.
```
