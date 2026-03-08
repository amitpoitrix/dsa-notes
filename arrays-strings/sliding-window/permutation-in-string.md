# Permutation in String — LC #567

**Pattern:** Sliding Window (Fixed) + Frequency Count
**Difficulty:** Medium
**Companies:** Amazon · Microsoft · Google

---

## Problem

Given strings `s1` and `s2`, return `true` if any permutation of `s1` is a substring of `s2`.

```
Input:  s1 = "ab", s2 = "eidbaooo"
Output: true   // "ba" is a permutation of "ab"

Input:  s1 = "ab", s2 = "eidboaoo"
Output: false
```

---

## Intuition

Identical to Find All Anagrams — fixed window of size `s1.length()`, check if any window in `s2` has same character frequencies as `s1`. Return true on first match.

---

## Algorithm

1. Build `s1Freq[26]`. Build `windowFreq[26]` from first `k` chars of `s2`.
2. If equal → return true.
3. Slide window: add right, remove left, compare.
4. Return false if no match found.

---

## Code — Java

```java
public boolean checkInclusion(String s1, String s2) {
    if (s1.length() > s2.length()) return false;

    int[] s1Freq = new int[26];
    int[] windowFreq = new int[26];
    int k = s1.length();

    for (char c : s1.toCharArray()) s1Freq[c - 'a']++;
    for (int i = 0; i < k; i++) windowFreq[s2.charAt(i) - 'a']++;

    if (Arrays.equals(s1Freq, windowFreq)) return true;

    for (int R = k; R < s2.length(); R++) {
        windowFreq[s2.charAt(R) - 'a']++;
        windowFreq[s2.charAt(R - k) - 'a']--;
        if (Arrays.equals(s1Freq, windowFreq)) return true;
    }
    return false;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | n = len(s2), O(26) comparison each step |
| Space | O(1) | Two int[26] arrays |

---

## Dry Run — s1 = "ab", s2 = "eidbaooo"

- s1Freq = {a:1, b:1}, k = 2
- Window "ei": {e:1,i:1} ✗
- Window "id": {i:1,d:1} ✗
- Window "db": {d:1,b:1} ✗
- Window "ba": {b:1,a:1} ✓ → return true

**Result:** true

---

## Edge Cases

- `s1.length() > s2.length()` → false.
- `s1 == s2` → true.

---

## Common Mistakes

- Same as Find All Anagrams — use `Arrays.equals()`, not `==`.

---

## Related Problems

- **Find All Anagrams (LC 438)** — same logic, return all indices instead
- **Minimum Window Substring (LC 76)** — variable window, must contain all chars
