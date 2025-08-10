# Frog Jump Problem — Brute Force vs Memoization (Single README)

## Problem
Given an array `height[]` where `height[i]` is the height of the `i`-th stone, a frog starts at stone `0` and can jump either **1** or **2** stones forward.  
Cost of a jump from stone `i` to stone `j` is:

cost = |height[j] - height[i]|

pgsql
Copy
Edit

Find the **minimum total cost** to reach the last stone.

---

## Table of Contents
- Brute-force (Recursive)
- Memoization (Top-down DP)
- Comparison (Complexity & Notes)
- Example (how to run)

---

## Brute-force (Recursive)
**Idea:** Explore every possible sequence of jumps (1 or 2 steps) recursively and track the minimum total cost.

**When to use:** Good to understand the problem and recursion. Not suitable for large inputs because it recomputes many states.

**Code (Java):**
```java
// Brute-force recursive approach
class SolutionBrute {
    // global min used to collect best result across recursive paths
    private int min = Integer.MAX_VALUE;

    private void solve(int[] nums, int n, int index, int cost) {
        // If reached last stone, update global minimum
        if (index == n - 1) {
            min = Math.min(min, cost);
            return;
        }

        // Jump by 1
        if (index + 1 < n) {
            int val = Math.abs(nums[index + 1] - nums[index]);
            solve(nums, n, index + 1, cost + val);
        }

        // Jump by 2
        if (index + 2 < n) {
            int val = Math.abs(nums[index + 2] - nums[index]);
            solve(nums, n, index + 2, cost + val);
        }
    }

    public int minCost(int[] height) {
        min = Integer.MAX_VALUE; // reset for each call
        solve(height, height.length, 0, 0);
        return min;
    }
}
Time Complexity: O(2^n) — each stone can branch to two options (exponential).
Space Complexity: O(n) — recursion stack.

Pros: Simple to implement and reason about.
Cons: Extremely slow for larger n (repetitive subproblem recomputation).

Memoization (Top-down Dynamic Programming)
Idea: Use a dp array to store the minimum cost from each index to the end. If a state is already computed, reuse it — avoids recomputation.

When to use: For large inputs; still uses recursion but avoids repeated work.

Code (Java):

java
Copy
Edit
// Memoization (top-down DP) approach
class SolutionMemo {
    public int solve(int[] nums, int n, int index, int[] dp) {
        // If reached last stone, cost is 0 from here
        if (index == n - 1) return 0;

        // If already computed, return
        if (dp[index] != -1) return dp[index];

        int cost1 = Integer.MAX_VALUE;
        int cost2 = Integer.MAX_VALUE;

        // Jump by 1
        if (index + 1 < n) {
            cost1 = Math.abs(nums[index + 1] - nums[index]) 
                    + solve(nums, n, index + 1, dp);
        }

        // Jump by 2
        if (index + 2 < n) {
            cost2 = Math.abs(nums[index + 2] - nums[index]) 
                    + solve(nums, n, index + 2, dp);
        }

        // store and return minimum cost from this index
        return dp[index] = Math.min(cost1, cost2);
    }

    public int minCost(int[] height) {
        int n = height.length;
        int[] dp = new int[n];
        java.util.Arrays.fill(dp, -1);
        return solve(height, n, 0, dp);
    }
}
Time Complexity: O(n) — each index computed at most once.
Space Complexity: O(n) — dp array + recursion stack.

Pros: Fast, simple top-down DP.
Cons: Recursion depth might still be O(n); can convert to iterative tabulation to avoid recursion if desired.

Comparison (Quick)
Approach	Time Complexity	Space Complexity	Suitable for
Brute-force	O(2^n)	O(n)	Small n, learning
Memoization	O(n)	O(n)	Large n, interview & production

Optional: Iterative (Tabulation) — space optimized
If you'd like a bottom-up iterative solution (no recursion) and O(1) extra space, here's a short idea:

pgsql
Copy
Edit
dp[0] = 0
dp[1] = |height[1] - height[0]|
for i from 2 to n-1:
    dp[i] = min(dp[i-1] + |h[i]-h[i-1]|, dp[i-2] + |h[i]-h[i-2]|)
answer = dp[n-1]
You can compress dp to two variables since we only need the last two dp values.


Understand base cases and why we reset min in the brute-force version.

Explain why memoization speeds things up (avoids recomputing the same index).

Be ready to convert memoized recursion to iterative DP (tabulation) if asked to remove recursion.

For follow-ups, discuss space optimization (keeping only last two dp values).

