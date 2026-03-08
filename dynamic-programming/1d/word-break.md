# Word Break — LC #139

**Pattern:** 1D DP
**Difficulty:** Medium
**Companies:** Google · Amazon · Facebook

---

## Problem

Given string `s` and dictionary `wordDict`, return true if `s` can be segmented into dictionary words.

```
Input:  s = "leetcode", wordDict = ["leet","code"]
Output: true
```

---

## Intuition

`dp[i]` = true if `s[0..i-1]` can be segmented. For each index `i`, check all `j < i`: if `dp[j]` is true and `s[j..i-1]` is in the dictionary, then `dp[i] = true`.

---

## Code — Java

```java
public boolean wordBreak(String s, List<String> wordDict) {
    Set<String> dict = new HashSet<>(wordDict);
    boolean[] dp = new boolean[s.length() + 1];
    dp[0] = true; // empty string

    for (int i = 1; i <= s.length(); i++) {
        for (int j = 0; j < i; j++) {
            if (dp[j] && dict.contains(s.substring(j, i))) {
                dp[i] = true;
                break;
            }
        }
    }
    return dp[s.length()];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n² * L) | n² substrings, each lookup O(L) |
| Space | O(n + D) | dp array + dict set |

---

## Edge Cases

- Single character words — works normally.
- Same word reused multiple times — dictionary is a set, reuse is allowed.

---

## Related Problems

- **Word Break II (LC 140)** — return all valid sentences
- **Decode Ways (LC 91)** — same DP structure
