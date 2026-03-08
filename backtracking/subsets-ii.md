# Subsets II — LC #90

**Pattern:** Backtracking + Skip Duplicates
**Difficulty:** Medium
**Companies:** Amazon · Facebook

---

## Problem

Given an integer array `nums` that may contain duplicates, return all possible subsets. No duplicate subsets in result.

```
Input:  nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

---

## Intuition

Same as Subsets I but sort first and skip duplicate values at the same recursion level. If `nums[i] == nums[i-1]` and `i > start`, skip (we already explored that branch with the same value).

---

## Algorithm

1. Sort `nums`.
2. Backtrack same as Subsets I.
3. Inside loop: if `i > start && nums[i] == nums[i-1]` → `continue`.

---

## Code — Java

```java
public List<List<Integer>> subsetsWithDup(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, 0, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] nums, int start, List<Integer> curr, List<List<Integer>> result) {
    result.add(new ArrayList<>(curr));

    for (int i = start; i < nums.length; i++) {
        if (i > start && nums[i] == nums[i - 1]) continue; // skip dup
        curr.add(nums[i]);
        backtrack(nums, i + 1, curr, result);
        curr.remove(curr.size() - 1);
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(2ⁿ * n) | Same as Subsets I |
| Space | O(n) | Recursion depth |

---

## Edge Cases

- All same elements `[2,2,2]` → `[[], [2], [2,2], [2,2,2]]`.

---

## Common Mistakes

- Checking `i > 0` instead of `i > start` — skips valid choices at the start of a new level.

---

## Related Problems

- **Subsets (LC 78)** — no duplicates version
- **Combination Sum II (LC 40)** — same dup-skip pattern with target
- **Permutations II (LC 47)** — dup-skip for permutations
