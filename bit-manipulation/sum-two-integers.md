# Sum of Two Integers — LC #371

**Pattern:** Bit Manipulation
**Difficulty:** Medium
**Companies:** Facebook · Amazon

---

## Problem

Calculate sum of two integers `a` and `b` without using `+` or `-` operators.

```
Input:  a = 1, b = 2
Output: 3
```

---

## Intuition

XOR gives sum without carry. AND gives carry positions, shift left by 1 to add carry. Repeat until no carry left.

---

## Code — Java

```java
public int getSum(int a, int b) {
    while (b != 0) {
        int carry = (a & b) << 1;
        a = a ^ b;
        b = carry;
    }
    return a;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(1) — at most 32 iterations |
| Space | O(1) |

---

## Related Problems

- **Reverse Bits (LC 190)** — bit ops
- **Number of 1 Bits (LC 191)** — bit counting
