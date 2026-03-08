# Decode Ways — LC #91

**Pattern:** 1D DP
**Difficulty:** Medium
**Companies:** Facebook · Amazon · Google

---

## Problem

A message encoded as digits (A=1, B=2, ..., Z=26). Given string `s`, count the number of ways to decode it.

```
Input:  s = "226"
Output: 3   // "BZ"(2,26), "VF"(22,6), "BBF"(2,2,6)
```

---

## Intuition

`dp[i]` = number of ways to decode `s[0..i-1]`. For each position:
- If `s[i-1] != '0'`, can decode as single digit: `dp[i] += dp[i-1]`.
- If `s[i-2..i-1]` forms a valid two-digit number (10-26): `dp[i] += dp[i-2]`.

---

## Code — Java

```java
public int numDecodings(String s) {
    int n = s.length();
    int[] dp = new int[n + 1];
    dp[0] = 1;
    dp[1] = s.charAt(0) == '0' ? 0 : 1;

    for (int i = 2; i <= n; i++) {
        int oneDigit = s.charAt(i - 1) - '0';
        int twoDigit = Integer.parseInt(s.substring(i - 2, i));

        if (oneDigit != 0) dp[i] += dp[i - 1];
        if (twoDigit >= 10 && twoDigit <= 26) dp[i] += dp[i - 2];
    }
    return dp[n];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n) |
| Space | O(n) — optimizable to O(1) |

---

## Edge Cases

- `"0"` → 0 ways. `"10"` → 1 way (`J`). `"30"` → 0 ways (30 > 26).

---

## Common Mistakes

- Not handling leading zeros — `'0'` alone or as second digit in two-digit number > 26 is invalid.

---

## Related Problems

- **Climbing Stairs (LC 70)** — same DP structure
- **Decode Ways II (LC 639)** — with `*` wildcard
