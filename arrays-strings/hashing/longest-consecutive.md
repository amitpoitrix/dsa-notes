# Longest Consecutive Sequence — LC #128

**Pattern:** HashSet
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta

---

## Problem

Given unsorted array `nums`, return the length of the longest consecutive elements sequence. Must run in O(n).

```
Input:  [100, 4, 200, 1, 3, 2]
Output: 4   // [1, 2, 3, 4]
```

---

## Intuition

Put all numbers in a HashSet. For each number, only start counting if it's the beginning of a sequence (i.e., `num - 1` is NOT in the set). Then count how far the sequence extends.

---

## Code — Java

```java
public int longestConsecutive(int[] nums) {
    Set<Integer> set = new HashSet<>();
    for (int n : nums) set.add(n);

    int maxLen = 0;

    for (int n : set) {
        if (!set.contains(n - 1)) { // start of a sequence
            int len = 1;
            while (set.contains(n + len)) len++;
            maxLen = Math.max(maxLen, len);
        }
    }
    return maxLen;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each number is visited at most twice |
| Space | O(n) | HashSet |

---

## Dry Run — [100, 4, 200, 1, 3, 2]

- set = {100, 4, 200, 1, 3, 2}
- 100: 99 not in set → count: 100 only → len=1
- 4: 3 in set → skip (not start)
- 200: 199 not in set → len=1
- 1: 0 not in set → count: 1,2,3,4 → len=4
- 3,2: in set, predecessors exist → skip

**Result:** 4

---

## Common Mistakes

- Iterating over `nums` instead of `set` — duplicates cause redundant work but still correct. Iterating set is cleaner.
- Sorting the array → O(n log n), violates the O(n) requirement.

---

## Related Problems

- **Longest Arithmetic Subsequence (LC 1027)** — generalized consecutive pattern
