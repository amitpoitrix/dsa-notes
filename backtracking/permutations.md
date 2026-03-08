# Permutations — LC #46

**Pattern:** Backtracking
**Difficulty:** Medium
**Companies:** Microsoft · Amazon · Facebook

---

## Problem

Given an array `nums` of distinct integers, return all possible permutations.

```
Input:  nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
```

---

## Intuition

Unlike subsets, order matters and every element must be used exactly once. Use a boolean `used[]` array. At each level, try every unused element. When current permutation length equals n, add to result.

---

## Algorithm

1. Use `backtrack(used[], curr[])`.
2. If `curr.size() == n` → add to result.
3. Loop all indices: if not used, mark used, add, recurse, unmark, remove.

---

## Code — Java

```java
public List<List<Integer>> permute(int[] nums) {
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
| Time  | O(n! * n) | n! permutations, each O(n) to copy |
| Space | O(n) | Recursion depth + used array |

---

## Edge Cases

- Single element → `[[x]]`.
- Two elements → `[[a,b],[b,a]]`.

---

## Common Mistakes

- Not resetting `used[i] = false` on backtrack — stale state contaminates other branches.
- Adding to result before length check.

---

## Related Problems

- **Permutations II (LC 47)** — with duplicates
- **Subsets (LC 78)** — order doesn't matter
- **Next Permutation (LC 31)** — find next lexicographic permutation
