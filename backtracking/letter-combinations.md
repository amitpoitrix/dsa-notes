# Letter Combinations of a Phone Number — LC #17

**Pattern:** Backtracking (Multi-branch)
**Difficulty:** Medium
**Companies:** Amazon · Google · Facebook

---

## Problem

Given a string of digits 2-9, return all possible letter combinations they could represent (T9 phone mapping). Return empty list if input is empty.

```
Input:  digits = "23"
Output: ["ad","ae","af","bd","be","bf","cd","ce","cf"]
```

---

## Intuition

Classic multi-branch backtracking. For each digit, try all its mapped letters. Recurse to the next digit. When current string length equals digits length, add to result.

---

## Code — Java

```java
public List<String> letterCombinations(String digits) {
    if (digits.isEmpty()) return new ArrayList<>();
    String[] map = {"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    List<String> result = new ArrayList<>();
    backtrack(digits, map, 0, new StringBuilder(), result);
    return result;
}

private void backtrack(String digits, String[] map, int idx, StringBuilder curr, List<String> result) {
    if (idx == digits.length()) {
        result.add(curr.toString());
        return;
    }
    for (char c : map[digits.charAt(idx) - '0'].toCharArray()) {
        curr.append(c);
        backtrack(digits, map, idx + 1, curr, result);
        curr.deleteCharAt(curr.length() - 1);
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(4ⁿ * n) | 4 letters max per digit, n digits |
| Space | O(n) | Recursion depth |

---

## Edge Cases

- Empty input → return `[]`.
- Single digit → return just its letters.

---

## Common Mistakes

- Not handling empty input — problem says return empty list, not `[""]`.

---

## Related Problems

- **Permutations (LC 46)** — all orderings
- **Generate Parentheses (LC 22)** — constrained multi-branch backtracking
