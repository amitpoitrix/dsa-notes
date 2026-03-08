# Valid Palindrome — LC #125

**Pattern:** Two Pointers (Opposite Ends)
**Difficulty:** Easy
**Companies:** Meta · Microsoft · Apple · Uber

---

## Problem

Given a string `s`, return `true` if it is a palindrome after converting to lowercase and removing all non-alphanumeric characters.

```
Input:  s = "A man, a plan, a canal: Panama"
Output: true   // "amanaplanacanalpanama" is a palindrome

Input:  s = "race a car"
Output: false
```

---

## Intuition

Use two pointers from both ends. Skip non-alphanumeric characters, then compare. If any mismatch found, return false. If pointers cross, it's a palindrome.

---

## Algorithm

1. Set `L = 0`, `R = s.length() - 1`.
2. While `L < R`:
   - Skip non-alphanumeric from left: while `L < R && !isAlphanumeric(s[L])` → `L++`.
   - Skip non-alphanumeric from right: while `L < R && !isAlphanumeric(s[R])` → `R--`.
   - If `toLowerCase(s[L]) != toLowerCase(s[R])` → return `false`.
   - `L++`, `R--`.
3. Return `true`.

---

## Code — Java

```java
public boolean isPalindrome(String s) {
    int L = 0, R = s.length() - 1;

    while (L < R) {
        while (L < R && !Character.isLetterOrDigit(s.charAt(L))) L++;
        while (L < R && !Character.isLetterOrDigit(s.charAt(R))) R--;

        if (Character.toLowerCase(s.charAt(L)) != Character.toLowerCase(s.charAt(R))) {
            return false;
        }
        L++;
        R--;
    }
    return true;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each character visited at most once |
| Space | O(1) | No extra string created |

---

## Dry Run — "A man, a plan, a canal: Panama"

After stripping non-alphanumeric: `amanaplanacanalpanama`

| L | R | s[L] | s[R] | Match? |
|---|---|------|------|--------|
| 0 | 19 | a | a | ✓ |
| 1 | 18 | m | m | ✓ |
| 2 | 17 | a | a | ✓ |
| ... | ... | ... | ... | ✓ all match |

**Result:** true

---

## Edge Cases

- **Empty string** `""` → true (empty string is a palindrome).
- **Single character** `"a"` → true.
- **All special characters** `".,!"` → true (after stripping, empty = palindrome).
- **Mixed case** `"Aa"` → true (case-insensitive).

---

## Common Mistakes

- Creating a cleaned string first → works but uses O(n) extra space. Two-pointer in-place is preferred.
- Forgetting `L < R` guard inside the inner skip loops → L or R can go out of bounds.

---

## Related Problems

- **Palindrome Linked List (LC 234)** — same idea, fast/slow pointer + reverse second half
- **Longest Palindromic Substring (LC 5)** — expand around center
- **Valid Palindrome II (LC 680)** — allow deleting one character
