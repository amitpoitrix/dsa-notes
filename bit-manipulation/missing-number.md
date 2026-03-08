# Missing Number — LC #268

**Pattern:** Bit Manipulation / Math
**Difficulty:** Easy
**Companies:** Amazon · Microsoft · Google

---

## Problem

Array contains n distinct numbers in range [0, n]. Find the missing one.

```
Input:  [3,0,1]
Output: 2
```

---

## Intuition

**XOR:** XOR all indices (0 to n) with all array values. Paired numbers cancel, leaving the missing number.

**Math:** Expected sum = n*(n+1)/2. Subtract actual sum.

---

## Code — Java (XOR)

```java
public int missingNumber(int[] nums) {
    int result = nums.length;
    for (int i = 0; i < nums.length; i++) {
        result ^= i ^ nums[i];
    }
    return result;
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

- **Single Number (LC 136)** — XOR trick
- **Find the Duplicate Number (LC 287)** — find extra, not missing
