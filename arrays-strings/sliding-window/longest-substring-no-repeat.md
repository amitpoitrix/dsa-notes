# Longest Substring Without Repeating Characters — LC #3

**Pattern:** Sliding Window (Variable)
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta · Microsoft · Uber

---

## Problem

Given string `s`, return the length of the longest substring without repeating characters.

```
Input:  s = "abcabcbb"
Output: 3   // "abc"

Input:  s = "pwwkew"
Output: 3   // "wke"
```

---

## Intuition

Expand window by moving `R` right. When a duplicate is found, shrink from `L` until the duplicate is removed. Use a HashMap to track the last seen index of each character for O(1) jump of `L`.

---

## Algorithm

1. Use `HashMap<Character, Integer>` to store last index of each char.
2. Set `L = 0`, `maxLen = 0`.
3. Loop `R` from 0 to n-1:
   - If `map` contains `s[R]` and its index >= `L` → jump `L` to `map.get(s[R]) + 1`.
   - Update `map.put(s[R], R)`.
   - Update `maxLen = max(maxLen, R - L + 1)`.
4. Return `maxLen`.

---

## Code — Java

```java
public int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> map = new HashMap<>();
    int maxLen = 0, L = 0;

    for (int R = 0; R < s.length(); R++) {
        char c = s.charAt(R);
        if (map.containsKey(c) && map.get(c) >= L) {
            L = map.get(c) + 1; // jump L past the duplicate
        }
        map.put(c, R);
        maxLen = Math.max(maxLen, R - L + 1);
    }
    return maxLen;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each character processed once |
| Space | O(min(n, 26)) | Map holds at most alphabet size chars |

---

## Dry Run — "abcabcbb"

| R | c | L | window | maxLen |
|---|---|---|--------|--------|
| 0 | a | 0 | "a"    | 1      |
| 1 | b | 0 | "ab"   | 2      |
| 2 | c | 0 | "abc"  | 3      |
| 3 | a | 1 | "bca"  | 3      |
| 4 | b | 2 | "cab"  | 3      |
| 5 | c | 3 | "abc"  | 3      |
| 6 | b | 5 | "cb"   | 3      |
| 7 | b | 7 | "b"    | 3      |

**Result:** 3

---

## Edge Cases

- Empty string → 0.
- All same chars `"aaaa"` → 1.
- All unique `"abcd"` → 4.

---

## Common Mistakes

- Using a Set and shrinking L one step at a time → O(n) worst case per step, still O(n) total but slower in practice.
- Not checking `map.get(c) >= L` → stale entries from before the current window cause L to jump backwards.

---

## Related Problems

- **Longest Substring with At Most K Distinct (LC 340)** — same pattern, extra constraint
- **Permutation in String (LC 567)** — fixed window + frequency
- **Minimum Window Substring (LC 76)** — variable window, find minimum
