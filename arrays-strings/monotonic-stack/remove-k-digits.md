# Remove K Digits — LC #402

**Pattern:** Greedy + Monotonic Increasing Stack
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Given string number `num` and integer `k`, remove `k` digits to make the smallest possible number.

```
Input:  num = "1432219", k = 3
Output: "1219"
```

---

## Intuition

To get the smallest number, greedily remove a digit when it's larger than the next digit (i.e., keep a monotonic increasing stack). Remove from the back if k still > 0 after the loop. Strip leading zeros.

---

## Code — Java

```java
public String removeKdigits(String num, int k) {
    Deque<Character> stack = new ArrayDeque<>();

    for (char c : num.toCharArray()) {
        while (k > 0 && !stack.isEmpty() && stack.peek() > c) {
            stack.pop();
            k--;
        }
        stack.push(c);
    }

    // remove remaining k digits from the end (largest)
    while (k-- > 0) stack.pop();

    // build result, remove leading zeros
    StringBuilder sb = new StringBuilder();
    while (!stack.isEmpty()) sb.append(stack.pollLast());

    String result = sb.toString().replaceAll("^0+", "");
    return result.isEmpty() ? "0" : result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each digit pushed and popped once |
| Space | O(n) | Stack |

---

## Common Mistakes

- Not handling leading zeros — use replaceAll or manual stripping.
- Not handling empty result — return "0" for cases like "10" k=2.

---

## Related Problems

- **Daily Temperatures (LC 739)** — same monotonic stack idea
- **Largest Number (LC 179)** — greedy ordering of numbers
