# Minimum Window Substring — LC #76

**Pattern:** Sliding Window (Variable)
**Difficulty:** Hard
**Companies:** Google · Meta · Amazon · Microsoft · Uber

---

## Problem

Given strings `s` and `t`, return the minimum window substring of `s` that contains all characters of `t`. Return `""` if no such window exists.

```
Input:  s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
```

---

## Intuition

Expand R to include all required characters. Once all are covered, shrink from L to minimize the window. Track what we "need" using a frequency map of `t`. Track how many distinct characters are currently "satisfied" (freq in window >= freq in t).

---

## Algorithm

1. Build `need` map from `t`. Set `required = need.size()` (distinct chars needed).
2. Use `window` map for current window frequencies.
3. Set `L = 0`, `formed = 0`, `minLen = ∞`, `minL = 0`.
4. Loop `R` from 0 to n-1:
   - Add `s[R]` to `window`.
   - If `window[s[R]] == need[s[R]]` → `formed++`.
   - While `formed == required`:
     - Update result if window is smaller.
     - Remove `s[L]` from window. If it drops below needed, `formed--`.
     - `L++`.
5. Return result string.

---

## Code — Java

```java
public String minWindow(String s, String t) {
    if (s.isEmpty() || t.isEmpty()) return "";

    Map<Character, Integer> need = new HashMap<>();
    for (char c : t.toCharArray()) need.put(c, need.getOrDefault(c, 0) + 1);

    int required = need.size();
    int L = 0, formed = 0;
    int minLen = Integer.MAX_VALUE, minL = 0;
    Map<Character, Integer> window = new HashMap<>();

    for (int R = 0; R < s.length(); R++) {
        char c = s.charAt(R);
        window.put(c, window.getOrDefault(c, 0) + 1);

        if (need.containsKey(c) && window.get(c).equals(need.get(c))) {
            formed++;
        }

        while (formed == required) {
            if (R - L + 1 < minLen) {
                minLen = R - L + 1;
                minL = L;
            }
            char left = s.charAt(L);
            window.put(left, window.get(left) - 1);
            if (need.containsKey(left) && window.get(left) < need.get(left)) {
                formed--;
            }
            L++;
        }
    }
    return minLen == Integer.MAX_VALUE ? "" : s.substring(minL, minL + minLen);
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n + m) | n = len(s), m = len(t), each char added/removed once |
| Space | O(m)     | need and window maps bounded by charset |

---

## Dry Run — s = "ADOBECODEBANC", t = "ABC"

- need = {A:1, B:1, C:1}, required = 3
- Expand until all 3 satisfied at R=5 → window "ADOBEC"
- Shrink from L: remove A → formed drops, expand again
- Eventually find "BANC" (len 4) as minimum

**Result:** "BANC"

---

## Edge Cases

- `t` has duplicate chars `"AA"` → need `{A:2}`, window must have freq >= 2.
- No valid window → return `""`.
- `s == t` → return `s`.

---

## Common Mistakes

- Using `==` instead of `.equals()` when comparing `Integer` objects from map — use `.equals()` or `int` unboxing.
- Using `need.size()` instead of tracking `formed` — distinct chars vs total chars covered are different.

---

## Related Problems

- **Longest Substring Without Repeating (LC 3)** — simpler variable window
- **Find All Anagrams (LC 438)** — fixed window version
- **Permutation in String (LC 567)** — fixed window, check if any window is a permutation
