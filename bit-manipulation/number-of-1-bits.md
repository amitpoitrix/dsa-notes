# Number of 1 Bits — LC #191

**Pattern:** Bit Manipulation (Brian Kernighan)
**Difficulty:** Easy
**Companies:** Apple · Amazon · Microsoft

---

## Problem

Return the number of set bits (1s) in a 32-bit integer. Also known as Hamming weight.

```
Input:  00000000000000000000000000001011
Output: 3
```

---

## Intuition

**Brian Kernighan's trick:** `n & (n-1)` clears the lowest set bit. Count how many times we can do this until n = 0.

---

## Code — Java

```java
public int hammingWeight(int n) {
    int count = 0;
    while (n != 0) {
        n &= (n - 1); // clear lowest set bit
        count++;
    }
    return count;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(k) — k = number of set bits |
| Space | O(1) |

---

## Related Problems

- **Counting Bits (LC 338)** — count for all numbers 0 to n
- **Reverse Bits (LC 190)** — bit manipulation
- **Power of Two (LC 231)** — power of 2 has exactly one set bit
