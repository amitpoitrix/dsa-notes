# Single Number — LC #136

**Pattern:** Bit Manipulation (XOR)
**Difficulty:** Easy
**Companies:** Amazon · Google · Facebook

---

## Problem

Every element appears twice except one. Find the one.

```
Input:  [4,1,2,1,2]
Output: 4
```

---

## Intuition

XOR of two equal numbers = 0. XOR with 0 = number itself. XOR all elements → duplicates cancel out, only the single number remains.

---

## Code — Java

```java
public int singleNumber(int[] nums) {
    int result = 0;
    for (int num : nums) result ^= num;
    return result;
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

- **Single Number II (LC 137)** — appears three times instead of twice
- **Single Number III (LC 260)** — two numbers appear once
- **Missing Number (LC 268)** — similar XOR trick
