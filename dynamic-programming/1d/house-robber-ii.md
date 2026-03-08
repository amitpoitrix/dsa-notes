# House Robber II — LC #213

**Pattern:** 1D DP (Circular)
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Same as House Robber but houses are in a circle — first and last are adjacent. Find max money.

```
Input:  nums = [2,3,2]
Output: 3
```

---

## Intuition

Can't rob both first and last house. So run House Robber I twice: once on `nums[0..n-2]` (exclude last) and once on `nums[1..n-1]` (exclude first). Return the max.

---

## Code — Java

```java
public int rob(int[] nums) {
    if (nums.length == 1) return nums[0];
    return Math.max(
        robRange(nums, 0, nums.length - 2),
        robRange(nums, 1, nums.length - 1)
    );
}

private int robRange(int[] nums, int l, int r) {
    int prev2 = 0, prev1 = 0;
    for (int i = l; i <= r; i++) {
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

## Common Mistakes

- Running on `nums[0..n-1]` and `nums[1..n]` — indices must correctly exclude one endpoint.

---

## Related Problems

- **House Robber (LC 198)** — linear version
- **House Robber III (LC 337)** — tree version
