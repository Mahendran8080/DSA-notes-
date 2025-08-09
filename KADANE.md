
# 📚 DSA Notes

## 📌 Maximum Subarray Sum — Kadane’s Algorithm

### ✅ Problem Statement

> Given an integer array `nums`, find the **contiguous subarray** (containing at least one number) which has the **largest sum** and return its sum.

---

### 🧠 Intuition

Kadane's Algorithm is a dynamic programming technique to solve this problem in **O(n)** time.  
It works by **tracking the maximum subarray sum ending at each index**, and **updating the global maximum** if the current sum exceeds it.

---

### 🧮 Algorithm

1. Initialize two variables:
   - `maxEndingHere = nums[0]` → Tracks the current subarray sum.
   - `maxSoFar = nums[0]` → Tracks the global maximum sum.

2. Iterate through the array starting from index `1`:
   - Update `maxEndingHere` as the maximum of:
     - Current element `nums[i]`
     - Sum of current element and previous subarray `maxEndingHere + nums[i]`
   - Update `maxSoFar` if `maxEndingHere` is greater than it.

3. Return `maxSoFar`.

---

### ✅ Code (Java)

```java
public class MaximumSubarray {
    public static int maxSubArray(int[] nums) {
        int maxEndingHere = nums[0];
        int maxSoFar = nums[0];

        for (int i = 1; i < nums.length; i++) {
            maxEndingHere = Math.max(nums[i], maxEndingHere + nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }

        return maxSoFar;
    }

    public static void main(String[] args) {
        int[] nums = {-2, 1, -3, 4, -1, 2, 1, -5, 4};
        System.out.println("Maximum Subarray Sum: " + maxSubArray(nums));
    }
}
