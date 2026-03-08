# Jump Game II — LC #45

**Pattern:** Greedy
**Difficulty:** Medium
**Companies:** Amazon · Google · Facebook

---

## Problem

Given `nums`, find minimum number of jumps to reach the last index. Guaranteed you can always reach it.

```
Input:  nums = [2,3,1,1,4]
Output: 2   // jump to index 1 (val 3), then to end
```

---

## Intuition

BFS levels / greedy. Track `currentEnd` (end of current jump range) and `farthest` (farthest reachable). When we reach `currentEnd`, we must jump — increment count and set `currentEnd = farthest`.

---

## Code — Java

```java
public int jump(int[] nums) {
    int jumps = 0, currentEnd = 0, farthest = 0;
    for (int i = 0; i < nums.length - 1; i++) {
        farthest = Math.max(farthest, i + nums[i]);
        if (i == currentEnd) {
            jumps++;
            currentEnd = farthest;
        }
    }
    return jumps;
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

- **Jump Game (LC 55)** — just check reachability
