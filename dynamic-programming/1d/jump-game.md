# Jump Game — LC #55

**Pattern:** Greedy / 1D DP
**Difficulty:** Medium
**Companies:** Amazon · Google · Microsoft

---

## Problem

Given array `nums` where `nums[i]` is max jump length at position `i`, determine if you can reach the last index.

```
Input:  nums = [2,3,1,1,4]   Output: true
Input:  nums = [3,2,1,0,4]   Output: false
```

---

## Intuition

Track `maxReach` — the farthest index reachable so far. For each index `i`, if `i > maxReach` we're stuck. Otherwise update `maxReach = max(maxReach, i + nums[i])`.

---

## Code — Java

```java
public boolean canJump(int[] nums) {
    int maxReach = 0;
    for (int i = 0; i < nums.length; i++) {
        if (i > maxReach) return false;
        maxReach = Math.max(maxReach, i + nums[i]);
    }
    return true;
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

- **Jump Game II (LC 45)** — minimum jumps to reach end
- **Jump Game III (LC 1306)** — can reach index with value 0
