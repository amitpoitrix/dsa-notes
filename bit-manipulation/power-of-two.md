# Power of Two — LC #231

**Pattern:** Bit Manipulation
**Difficulty:** Easy
**Companies:** Amazon · Google

---

## Problem

Given integer `n`, return true if it is a power of two.

```
Input:  n = 16   Output: true
Input:  n = 3    Output: false
```

---

## Intuition

Powers of 2 have exactly one set bit. `n & (n-1)` clears the lowest set bit. If result is 0 and `n > 0`, then `n` has only one set bit → power of 2.

---

## Code — Java

```java
public boolean isPowerOfTwo(int n) {
    return n > 0 && (n & (n - 1)) == 0;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(1) |
| Space | O(1) |

---

## Related Problems

- **Power of Three (LC 326)** — math approach (no bit trick)
- **Number of 1 Bits (LC 191)** — count set bits
