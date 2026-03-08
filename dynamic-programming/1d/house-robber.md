# House Robber — LC #198

**Pattern:** 1D DP
**Difficulty:** Medium
**Companies:** Amazon · Google · Microsoft

---

## Problem

Houses in a row, each with some money. Can't rob two adjacent houses. Find max money you can rob.

```
Input:  nums = [2,7,9,3,1]
Output: 12   // 2 + 9 + 1
```

---

## Intuition

For each house `i`: either rob it (get `nums[i] + dp[i-2]`) or skip it (`dp[i-1]`). Take the max. Optimize to O(1) space with two variables.

---

## Code — Java

```java
public int rob(int[] nums) {
    if (nums.length == 1) return nums[0];
    int prev2 = nums[0], prev1 = Math.max(nums[0], nums[1]);
    for (int i = 2; i < nums.length; i++) {
        int curr = Math.max(prev1, prev2 + nums[i]);
        prev2 = prev1;
        prev1 = curr;
    }
    return prev1;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n) |
| Space | O(1) |

---

## Related Problems

- **House Robber II (LC 213)** — circular arrangement
- **House Robber III (LC 337)** — tree structure
- **Climbing Stairs (LC 70)** — same DP recurrence
