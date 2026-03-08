# Pow(x, n) — LC #50

**Pattern:** Fast Exponentiation (Bit Manipulation)
**Difficulty:** Medium
**Companies:** Google · Amazon · Facebook

---

## Problem

Implement `pow(x, n)` — x raised to the power n.

```
Input:  x = 2.0, n = 10   Output: 1024.0
Input:  x = 2.0, n = -2   Output: 0.25
```

---

## Intuition

Repeated squaring: `x^n = (x^(n/2))^2` if n even, `x * (x^(n/2))^2` if n odd. This reduces multiplications from O(n) to O(log n). Handle negative n by inverting x.

---

## Code — Java

```java
public double myPow(double x, int n) {
    long N = n; // avoid overflow for Integer.MIN_VALUE
    if (N < 0) { x = 1 / x; N = -N; }
    double result = 1;
    while (N > 0) {
        if ((N & 1) == 1) result *= x; // odd exponent
        x *= x;
        N >>= 1;
    }
    return result;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(log n) |
| Space | O(1) |

---

## Edge Cases

- `n = Integer.MIN_VALUE` → `-n` overflows. Use `long N = n`.
- `x = 0, n = 0` → convention: return 1.

---

## Common Mistakes

- Not casting `n` to `long` before negating — `Integer.MIN_VALUE * -1` overflows.

---

## Related Problems

- **Fast Matrix Exponentiation** — same idea for matrix powers
- **Super Pow (LC 372)** — modular exponentiation
