# Single Number II — LC #137

**Pattern:** Bit Manipulation
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Every element appears three times except one which appears once. Find it without using extra memory.

```
Input:  [2,2,3,2]
Output: 3
```

---

## Intuition

Count bits at each position mod 3. If count % 3 != 0, the single number has that bit set. Alternatively: use two variables `ones` and `twos` tracking bits seen once and twice. A bit appears in `ones` first, then `twos`, then resets to 0.

---

## Code — Java

```java
public int singleNumber(int[] nums) {
    int ones = 0, twos = 0;
    for (int num : nums) {
        ones = (ones ^ num) & ~twos;
        twos = (twos ^ num) & ~ones;
    }
    return ones;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n) |
| Space | O(1) |

---

## Related Problems

- **Single Number (LC 136)** — appears twice
- **Single Number III (LC 260)** — two singles
