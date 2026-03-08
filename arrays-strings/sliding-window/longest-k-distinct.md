# Longest Substring with At Most K Distinct Characters — LC #340

**Pattern:** Sliding Window (Variable)
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta

---

## Problem

Given string `s` and integer `k`, return the length of the longest substring that contains at most `k` distinct characters.

```
Input:  s = "eceba", k = 2
Output: 3   // "ece"

Input:  s = "aa", k = 1
Output: 2   // "aa"
```

---

## Intuition

Expand R. Track character frequencies in a HashMap. When distinct count exceeds `k`, shrink from L until we're back to `k` distinct characters.

---

## Algorithm

1. Use `HashMap<Character, Integer>` for frequency count.
2. Set `L = 0`, `maxLen = 0`.
3. Loop `R` from 0 to n-1:
   - Add `s[R]` to map, increment count.
   - While `map.size() > k`:
     - Decrement `s[L]` count. If count == 0, remove from map.
     - `L++`.
   - Update `maxLen = max(maxLen, R - L + 1)`.
4. Return `maxLen`.

---

## Code — Java

```java
public int lengthOfLongestSubstringKDistinct(String s, int k) {
    Map<Character, Integer> freq = new HashMap<>();
    int L = 0, maxLen = 0;

    for (int R = 0; R < s.length(); R++) {
        char c = s.charAt(R);
        freq.put(c, freq.getOrDefault(c, 0) + 1);

        while (freq.size() > k) {
            char left = s.charAt(L);
            freq.put(left, freq.get(left) - 1);
            if (freq.get(left) == 0) freq.remove(left);
            L++;
        }
        maxLen = Math.max(maxLen, R - L + 1);
    }
    return maxLen;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each char added and removed at most once |
| Space | O(k) | Map holds at most k+1 chars at any time |

---

## Dry Run — "eceba", k = 2

| R | c | freq             | L | window | maxLen |
|---|---|------------------|---|--------|--------|
| 0 | e | {e:1}            | 0 | "e"    | 1      |
| 1 | c | {e:1, c:1}       | 0 | "ec"   | 2      |
| 2 | e | {e:2, c:1}       | 0 | "ece"  | 3      |
| 3 | b | {e:2,c:1,b:1}→shrink| 2 | "eb" | 3      |
| 4 | a | {e:1,b:1,a:1}→shrink| 3| "ba" | 3      |

**Result:** 3

---

## Edge Cases

- `k == 0` → return 0.
- `k >= distinct chars in s` → return `s.length()`.

---

## Common Mistakes

- Not removing the key when count hits 0 — map size stays inflated, while loop never terminates.

---

## Related Problems

- **Longest Substring Without Repeating (LC 3)** — k = all unique (each at most 1)
- **Fruits Into Baskets (LC 904)** — exact same problem, k = 2
- **Minimum Window Substring (LC 76)** — must contain all chars, find min length
