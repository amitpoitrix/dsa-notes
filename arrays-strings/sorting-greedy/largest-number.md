# Largest Number — LC #179

**Pattern:** Custom Sort
**Difficulty:** Medium
**Companies:** Amazon · Google · Microsoft

---

## Problem

Given non-negative integers, arrange them to form the largest number.

```
Input:  [3, 30, 34, 5, 9]
Output: "9534330"
```

---

## Intuition

For two numbers a and b, compare `str(a)+str(b)` vs `str(b)+str(a)`. Use this as the custom comparator.

---

## Code — Java

```java
public String largestNumber(int[] nums) {
    String[] strs = new String[nums.length];
    for (int i = 0; i < nums.length; i++) strs[i] = String.valueOf(nums[i]);

    Arrays.sort(strs, (a, b) -> (b + a).compareTo(a + b));

    if (strs[0].equals("0")) return "0"; // all zeros

    return String.join("", strs);
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log n * k) | k = average string length |
| Space | O(n)           | String array |

---

## Common Mistakes

- Forgetting the all-zeros edge case — `[0,0]` should return "0" not "00".
