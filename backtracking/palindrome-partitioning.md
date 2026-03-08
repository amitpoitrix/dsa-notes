# Palindrome Partitioning — LC #131

**Pattern:** Backtracking + DP
**Difficulty:** Medium
**Companies:** Amazon · Google · Facebook

---

## Problem

Given string `s`, partition it such that every substring is a palindrome. Return all possible partitionings.

```
Input:  s = "aab"
Output: [["a","a","b"],["aa","b"]]
```

---

## Intuition

Backtracking: try every prefix of the current string. If the prefix is a palindrome, add it to current partition and recurse on the remaining string. When index reaches end, add the full partition to result.

---

## Code — Java

```java
public List<List<String>> partition(String s) {
    List<List<String>> result = new ArrayList<>();
    backtrack(s, 0, new ArrayList<>(), result);
    return result;
}

private void backtrack(String s, int start, List<String> curr, List<List<String>> result) {
    if (start == s.length()) {
        result.add(new ArrayList<>(curr));
        return;
    }
    for (int end = start + 1; end <= s.length(); end++) {
        String sub = s.substring(start, end);
        if (isPalindrome(sub)) {
            curr.add(sub);
            backtrack(s, end, curr, result);
            curr.remove(curr.size() - 1);
        }
    }
}

private boolean isPalindrome(String s) {
    int l = 0, r = s.length() - 1;
    while (l < r) {
        if (s.charAt(l++) != s.charAt(r--)) return false;
    }
    return true;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(2ⁿ * n) | 2ⁿ partitions, palindrome check O(n) |
| Space | O(n) | Recursion depth |

---

## Optimization

Precompute a 2D `dp[i][j]` palindrome table in O(n²) to make each palindrome check O(1) instead of O(n).

---

## Common Mistakes

- Checking palindrome inside tight loop without caching — precompute DP table for large inputs.

---

## Related Problems

- **Palindrome Partitioning II (LC 132)** — minimum cuts version (DP)
- **Subsets (LC 78)** — all partitions without palindrome constraint
