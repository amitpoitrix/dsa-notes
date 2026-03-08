# Combination Sum II — LC #40

**Pattern:** Backtracking + Skip Duplicates
**Difficulty:** Medium
**Companies:** Amazon · Bloomberg

---

## Problem

Given `candidates` (may have duplicates) and `target`, return all unique combinations where each number used once and sum equals target.

```
Input:  candidates = [10,1,2,7,6,1,5], target = 8
Output: [[1,1,6],[1,2,5],[1,7],[2,6]]
```

---

## Intuition

Sort + backtrack with `i+1` (each element once). Skip duplicates at same level: `if i > start && candidates[i] == candidates[i-1] → continue`.

---

## Code — Java

```java
public List<List<Integer>> combinationSum2(int[] candidates, int target) {
    Arrays.sort(candidates);
    List<List<Integer>> result = new ArrayList<>();
    backtrack(candidates, target, 0, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] candidates, int remain, int start, List<Integer> curr, List<List<Integer>> result) {
    if (remain == 0) { result.add(new ArrayList<>(curr)); return; }
    for (int i = start; i < candidates.length; i++) {
        if (candidates[i] > remain) break;
        if (i > start && candidates[i] == candidates[i - 1]) continue; // skip dup
        curr.add(candidates[i]);
        backtrack(candidates, remain - candidates[i], i + 1, curr, result);
        curr.remove(curr.size() - 1);
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(2ⁿ) | Worst case all subsets |
| Space | O(n) | Recursion depth |

---

## Common Mistakes

- `i > start` not `i > 0` for dup-skip — same reasoning as Subsets II.

---

## Related Problems

- **Combination Sum (LC 39)** — unlimited reuse, no duplicates
- **Subsets II (LC 90)** — same dup-skip pattern
