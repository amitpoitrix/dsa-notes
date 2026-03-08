# Find All Anagrams in a String — LC #438

**Pattern:** Sliding Window (Fixed) + Frequency Count
**Difficulty:** Medium
**Companies:** Amazon · Meta · Google

---

## Problem

Given strings `s` and `p`, return all start indices of `p`'s anagrams in `s`.

```
Input:  s = "cbaebabacd", p = "abc"
Output: [0, 6]   // "cba" at 0, "bac" at 6
```

---

## Intuition

An anagram is a permutation — same character frequencies. Use a fixed window of size `p.length()`. Slide it across `s` comparing frequency arrays. When frequencies match, record the index.

Comparing two arrays of size 26 each step is O(26) = O(1).

---

## Algorithm

1. Build `pFreq[26]` from `p` and `windowFreq[26]` from first `k` chars of `s`.
2. If `pFreq == windowFreq`, add index 0.
3. Slide window from index `k` to `n-1`:
   - Add `s[R]`, remove `s[R-k]`.
   - If frequencies match, add `R - k + 1`.
4. Return result.

---

## Code — Java

```java
public List<Integer> findAnagrams(String s, String p) {
    List<Integer> result = new ArrayList<>();
    if (s.length() < p.length()) return result;

    int[] pFreq = new int[26];
    int[] windowFreq = new int[26];
    int k = p.length();

    for (char c : p.toCharArray()) pFreq[c - 'a']++;
    for (int i = 0; i < k; i++) windowFreq[s.charAt(i) - 'a']++;

    if (Arrays.equals(pFreq, windowFreq)) result.add(0);

    for (int R = k; R < s.length(); R++) {
        windowFreq[s.charAt(R) - 'a']++;
        windowFreq[s.charAt(R - k) - 'a']--;
        if (Arrays.equals(pFreq, windowFreq)) result.add(R - k + 1);
    }
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each step does O(26) = O(1) comparison |
| Space | O(1) | Two fixed-size arrays of 26 |

---

## Dry Run — s = "cbaebabacd", p = "abc"

- pFreq = {a:1, b:1, c:1}
- Initial window "cba": windowFreq = {a:1,b:1,c:1} ✓ → add 0
- Slide to "bae": {b:1,a:1,e:1} ✗
- Slide to "aeb": {a:1,e:1,b:1} ✗
- Slide to "eba": {e:1,b:1,a:1} ✗
- Slide to "bab": {b:2,a:1} ✗
- Slide to "aba": {a:2,b:1} ✗
- Slide to "bac": {b:1,a:1,c:1} ✓ → add 6

**Result:** [0, 6]

---

## Edge Cases

- `p.length() > s.length()` → return empty list.
- `s == p` → return `[0]`.

---

## Common Mistakes

- Using HashMap instead of int[26] — works but slower due to boxing overhead.
- Checking `pFreq.equals(windowFreq)` on arrays — use `Arrays.equals()`.

---

## Related Problems

- **Permutation in String (LC 567)** — return boolean instead of indices, otherwise identical
- **Minimum Window Substring (LC 76)** — variable window
- **Longest Substring Without Repeating (LC 3)** — variable window
