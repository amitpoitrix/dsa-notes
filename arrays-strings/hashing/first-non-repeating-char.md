# First Non-Repeating Character — LC #387

**Pattern:** Frequency Count + Index
**Difficulty:** Easy
**Companies:** Amazon · Microsoft · Bloomberg

---

## Problem

Given string `s`, find the first non-repeating character and return its index. Return -1 if none.

```
Input:  s = "leetcode"
Output: 0   // 'l' appears once

Input:  s = "aabb"
Output: -1
```

---

## Code — Java

```java
public int firstUniqChar(String s) {
    int[] freq = new int[26];
    for (char c : s.toCharArray()) freq[c - 'a']++;

    for (int i = 0; i < s.length(); i++) {
        if (freq[s.charAt(i) - 'a'] == 1) return i;
    }
    return -1;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Two passes |
| Space | O(1) | Fixed array of 26 |

---

## Common Mistakes

- Returning the character instead of its index.

---

## Related Problems

- **Valid Anagram (LC 242)** — same frequency count technique
- **First Unique Character in a Stream** — use LinkedHashMap to maintain order
