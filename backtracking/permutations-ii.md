# Permutations II — LC #47

**Pattern:** Backtracking + Skip Duplicates
**Difficulty:** Medium
**Companies:** Microsoft · Amazon

---

## Problem

Given a collection `nums` that might contain duplicates, return all unique permutations.

```
Input:  nums = [1,1,2]
Output: [[1,1,2],[1,2,1],[2,1,1]]
```

---

## Intuition

Sort first. Use `used[]` array. Skip duplicates: if `nums[i] == nums[i-1]` and `!used[i-1]`, it means we're at the same level and already used that value in a previous branch — skip to avoid duplicates.

---

## Code — Java

```java
public List<List<Integer>> permuteUnique(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, new boolean[nums.length], new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] nums, boolean[] used, List<Integer> curr, List<List<Integer>> result) {
    if (curr.size() == nums.length) {
        result.add(new ArrayList<>(curr));
        return;
    }
    for (int i = 0; i < nums.length; i++) {
        if (used[i]) continue;
        // skip duplicate: same value, previous not used in current path
        if (i > 0 && nums[i] == nums[i - 1] && !used[i - 1]) continue;
        used[i] = true;
        curr.add(nums[i]);
        backtrack(nums, used, curr, result);
        curr.remove(curr.size() - 1);
        used[i] = false;
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n! * n) | Worst case all unique |
| Space | O(n) | Recursion + used array |

---

## Common Mistakes

- The dup-skip condition `!used[i-1]` is tricky — it means: same value as previous, and previous hasn't been placed yet in current path (same level), so we already explored this branch.

---

## Related Problems

- **Permutations (LC 46)** — no duplicates
- **Subsets II (LC 90)** — dup-skip for subsets
