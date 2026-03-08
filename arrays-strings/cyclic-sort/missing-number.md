# Missing Number — LC #268

**Pattern:** XOR / Gauss Sum
**Difficulty:** Easy
**Companies:** Amazon · Microsoft · Google

---

## Problem

Given array `nums` with `n` distinct numbers from `[0, n]`, find the missing number.

```
Input:  [3, 0, 1]
Output: 2
```

---

## Approach 1: Gauss Sum

```java
public int missingNumber(int[] nums) {
    int n = nums.length;
    int expected = n * (n + 1) / 2;
    int actual = 0;
    for (int num : nums) actual += num;
    return expected - actual;
}
```

---

## Approach 2: XOR

```java
public int missingNumber(int[] nums) {
    int xor = nums.length;
    for (int i = 0; i < nums.length; i++) xor ^= i ^ nums[i];
    return xor;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(1) | |

---

## Related Problems

- **Find the Duplicate Number (LC 287)** — cyclic detection
- **Set Mismatch (LC 645)** — both missing and duplicate
