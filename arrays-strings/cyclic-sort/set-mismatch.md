# Set Mismatch — LC #645

**Pattern:** Cyclic Sort / Index Marking
**Difficulty:** Easy
**Companies:** Amazon · Microsoft

---

## Problem

Array `nums` should contain `[1, n]` but one number is duplicated and one is missing. Find `[duplicate, missing]`.

```
Input:  [1, 2, 2, 4]
Output: [2, 3]
```

---

## Approach: Negation Marking

```java
public int[] findErrorNums(int[] nums) {
    int dup = -1, missing = -1;

    for (int num : nums) {
        int idx = Math.abs(num) - 1;
        if (nums[idx] < 0) dup = Math.abs(num);
        else nums[idx] = -nums[idx];
    }

    for (int i = 0; i < nums.length; i++) {
        if (nums[i] > 0) missing = i + 1;
    }
    return new int[]{dup, missing};
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Two passes |
| Space | O(1) | |

---

## Related Problems

- **Find All Duplicates (LC 442)** — same negation technique
- **Missing Number (LC 268)** — only missing, no duplicate
