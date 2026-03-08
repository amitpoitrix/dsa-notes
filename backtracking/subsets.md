# Subsets — LC #78

**Pattern:** Backtracking
**Difficulty:** Medium
**Companies:** Facebook · Amazon · Google

---

## Problem

Given an integer array `nums` of unique elements, return all possible subsets (the power set). No duplicates in result.

```
Input:  nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
```

---

## Intuition

At each index, we have two choices: include the element or skip it. Use backtracking — add current subset to result at every recursive call (not just leaves). Start index prevents reuse of previous elements.

---

## Algorithm

1. Start with empty subset, call `backtrack(0, [])`.
2. At each call: add current subset to result.
3. Loop `i` from `start` to `n-1`: add `nums[i]`, recurse with `i+1`, then remove `nums[i]`.

---

## Code — Java

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, 0, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] nums, int start, List<Integer> curr, List<List<Integer>> result) {
    result.add(new ArrayList<>(curr)); // add at every node, not just leaves

    for (int i = start; i < nums.length; i++) {
        curr.add(nums[i]);
        backtrack(nums, i + 1, curr, result);
        curr.remove(curr.size() - 1); // backtrack
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(2ⁿ * n) | 2ⁿ subsets, each costs O(n) to copy |
| Space | O(n) | Recursion depth |

---

## Edge Cases

- Empty input → `[[]]`.
- Single element → `[[], [x]]`.

---

## Common Mistakes

- Not copying `curr` when adding to result — `result.add(curr)` adds a reference, not a snapshot.
- Starting `i` from 0 instead of `start` — causes duplicates.

---

## Related Problems

- **Subsets II (LC 90)** — with duplicates, need to sort + skip
- **Combination Sum (LC 39)** — subsets with target sum constraint
- **Permutations (LC 46)** — order matters
