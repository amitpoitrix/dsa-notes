# Generate Parentheses — LC #22

**Pattern:** Backtracking (Count-based)
**Difficulty:** Medium
**Companies:** Google · Amazon · Facebook

---

## Problem

Given `n` pairs of parentheses, generate all combinations of well-formed parentheses.

```
Input:  n = 3
Output: ["((()))","(()())","(())()","()(())","()()()"]
```

---

## Intuition

Track `open` count and `close` count. Rules:
- Can add `(` if `open < n`.
- Can add `)` if `close < open`.
When both equal `n`, add to result.

---

## Code — Java

```java
public List<String> generateParenthesis(int n) {
    List<String> result = new ArrayList<>();
    backtrack(n, 0, 0, new StringBuilder(), result);
    return result;
}

private void backtrack(int n, int open, int close, StringBuilder curr, List<String> result) {
    if (curr.length() == 2 * n) {
        result.add(curr.toString());
        return;
    }
    if (open < n) {
        curr.append('(');
        backtrack(n, open + 1, close, curr, result);
        curr.deleteCharAt(curr.length() - 1);
    }
    if (close < open) {
        curr.append(')');
        backtrack(n, open, close + 1, curr, result);
        curr.deleteCharAt(curr.length() - 1);
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(4ⁿ/√n) | Catalan number of valid sequences |
| Space | O(n) | Recursion depth = 2n |

---

## Common Mistakes

- Generating all 2^2n combinations and filtering — correct but wasteful. Constraint-based generation only produces valid strings.

---

## Related Problems

- **Letter Combinations (LC 17)** — multi-branch backtracking
- **Valid Parentheses (LC 20)** — validate a given string
