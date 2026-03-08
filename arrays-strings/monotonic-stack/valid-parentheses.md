# Valid Parentheses — LC #20

**Pattern:** Stack
**Difficulty:** Easy
**Companies:** Google · Amazon · Meta · Microsoft · Everywhere

---

## Problem

Given string `s` with `()[]{}`, determine if it's valid. Open brackets must be closed in the correct order.

```
Input:  "()[]{}"  → true
Input:  "([)]"    → false
Input:  "{[]}"    → true
```

---

## Code — Java

```java
public boolean isValid(String s) {
    Deque<Character> stack = new ArrayDeque<>();

    for (char c : s.toCharArray()) {
        if (c == '(' || c == '[' || c == '{') {
            stack.push(c);
        } else {
            if (stack.isEmpty()) return false;
            char top = stack.pop();
            if (c == ')' && top != '(') return false;
            if (c == ']' && top != '[') return false;
            if (c == '}' && top != '{') return false;
        }
    }
    return stack.isEmpty();
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(n) | Stack |

---

## Common Mistakes

- Not checking `stack.isEmpty()` before popping — throws exception.
- Not checking `stack.isEmpty()` at the end — `"((("` returns true incorrectly.
