# Reverse Bits — LC #190

**Pattern:** Bit Manipulation
**Difficulty:** Easy
**Companies:** Apple · Amazon

---

## Problem

Reverse bits of a 32-bit unsigned integer.

```
Input:  00000010100101000001111010011100
Output: 00111001011110000010100101000000 (964176192)
```

---

## Code — Java

```java
public int reverseBits(int n) {
    int result = 0;
    for (int i = 0; i < 32; i++) {
        result = (result << 1) | (n & 1);
        n >>= 1;
    }
    return result;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(32) = O(1) |
| Space | O(1) |

---

## Key Steps

Each iteration: shift result left (make room), OR in the LSB of n, then shift n right.

---

## Related Problems

- **Number of 1 Bits (LC 191)** — count set bits
- **Counting Bits (LC 338)** — count for range
