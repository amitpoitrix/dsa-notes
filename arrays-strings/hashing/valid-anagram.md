# Valid Anagram — LC #242

**Pattern:** Frequency Count
**Difficulty:** Easy
**Companies:** Amazon · Microsoft · Google

---

## Problem

Given strings `s` and `t`, return `true` if `t` is an anagram of `s`.

```
Input:  s = "anagram", t = "nagaram"
Output: true

Input:  s = "rat", t = "car"
Output: false
```

---

## Intuition

Two strings are anagrams if they have identical character frequencies. Use an int[26] array — increment for s, decrement for t. If all zeros at the end, they're anagrams.

---

## Code — Java

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;

    int[] count = new int[26];
    for (char c : s.toCharArray()) count[c - 'a']++;
    for (char c : t.toCharArray()) count[c - 'a']--;

    for (int n : count) if (n != 0) return false;
    return true;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Two passes through strings |
| Space | O(1) | Fixed array of 26 |

---

## Follow-up

If inputs contain Unicode characters, use `HashMap<Character, Integer>` instead of int[26].

---

## Related Problems

- **Group Anagrams (LC 49)** — group all anagrams together
- **Find All Anagrams (LC 438)** — find anagram positions in string
