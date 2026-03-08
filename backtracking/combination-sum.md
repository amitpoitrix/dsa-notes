# Combination Sum — LC #39

**Pattern:** Backtracking
**Difficulty:** Medium
**Companies:** Amazon · Google · Facebook

---

## Problem

Given distinct integers `candidates` and a `target`, return all unique combinations where chosen numbers sum to target. Same number may be used unlimited times.

```
Input:  candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
```

---

## Intuition

Backtracking with `start` index. Since we can reuse elements, pass `i` (not `i+1`) when recursing. Prune: if remaining target < 0, stop. Sort candidates to enable early termination.

---

## Code — Java

```java
public List<List<Integer>> combinationSum(int[] candidates, int target) {
    Arrays.sort(candidates);
    List<List<Integer>> result = new ArrayList<>();
    backtrack(candidates, target, 0, new ArrayList<>(), result);
    return result;
}

private void backtrack(int[] candidates, int remain, int start, List<Integer> curr, List<List<Integer>> result) {
    if (remain == 0) { result.add(new ArrayList<>(curr)); return; }
    for (int i = start; i < candidates.length; i++) {
        if (candidates[i] > remain) break; // pruning
        curr.add(candidates[i]);
        backtrack(candidates, remain - candidates[i], i, curr, result); // i not i+1 (reuse allowed)
        curr.remove(curr.size() - 1);
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n^(T/M)) | T=target, M=min candidate |
| Space | O(T/M) | Max recursion depth |

---

## Common Mistakes

- Passing `i+1` instead of `i` — prevents reuse of the same element.
- Not sorting — can't use `break` for pruning without sorted order.

---

## Related Problems

- **Combination Sum II (LC 40)** — each element used once, has duplicates
- **Combination Sum III (LC 216)** — exactly k numbers summing to n
