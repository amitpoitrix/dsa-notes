# Find All Duplicates in an Array — LC #442

**Pattern:** Index Marking (Negation)
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Given array where `1 <= nums[i] <= n`, find all elements that appear twice. O(n) time, O(1) space.

```
Input:  [4, 3, 2, 7, 8, 2, 3, 1]
Output: [2, 3]
```

---

## Intuition

Use the sign of `nums[index]` as a visited marker. For each `nums[i]`, go to index `|nums[i]| - 1`. If it's negative, we've been here → it's a duplicate. Otherwise negate it.

---

## Code — Java

```java
public List<Integer> findDuplicates(int[] nums) {
    List<Integer> result = new ArrayList<>();

    for (int i = 0; i < nums.length; i++) {
        int idx = Math.abs(nums[i]) - 1;
        if (nums[idx] < 0) {
            result.add(idx + 1);
        } else {
            nums[idx] = -nums[idx];
        }
    }
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(1) | Output not counted |

---

## Common Mistakes

- Using `nums[i]` as index directly — must use `abs(nums[i]) - 1` since numbers are 1-indexed.

---

## Related Problems

- **Find the Duplicate Number (LC 287)** — single duplicate, Floyd's cycle
- **First Missing Positive (LC 41)** — similar index trick
