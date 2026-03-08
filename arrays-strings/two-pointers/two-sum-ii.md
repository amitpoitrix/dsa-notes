# Two Sum II — LC #167

**Pattern:** Two Pointers (Opposite Ends)
**Difficulty:** Easy
**Companies:** Amazon · Microsoft · Adobe

---

## Problem

Given a **1-indexed** sorted array `numbers`, find two numbers that add up to `target`. Return their indices as `[index1, index2]`. Exactly one solution exists.

```
Input:  numbers = [2, 7, 11, 15], target = 9
Output: [1, 2]   // numbers[1] + numbers[2] = 2 + 7 = 9
```

---

## Intuition

Array is already sorted. Start with one pointer at the left (smallest) and one at the right (largest). If their sum is too big, move right pointer left. If too small, move left pointer right. Since exactly one solution exists, we will always find it.

No need for a HashMap like Two Sum I — sorting gives us directional control.

---

## Algorithm

1. Set `L = 0`, `R = n - 1`.
2. While `L < R`:
   - `sum == target` → return `[L+1, R+1]` (1-indexed)
   - `sum < target` → `L++`
   - `sum > target` → `R--`

---

## Code — Java

```java
public int[] twoSum(int[] numbers, int target) {
    int L = 0, R = numbers.length - 1;

    while (L < R) {
        int sum = numbers[L] + numbers[R];

        if (sum == target) {
            return new int[]{L + 1, R + 1}; // 1-indexed
        } else if (sum < target) {
            L++;
        } else {
            R--;
        }
    }
    return new int[]{};  // never reached, problem guarantees a solution
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass with two pointers |
| Space | O(1) | No extra data structures |

---

## Dry Run — [2, 7, 11, 15], target = 9

| L | R | sum | Action |
|---|---|-----|--------|
| 0 (2) | 3 (15) | 17 | R-- |
| 0 (2) | 2 (11) | 13 | R-- |
| 0 (2) | 1 (7)  | 9 ✓ | return [1, 2] |

---

## Edge Cases

- **Two elements** `[1, 3], target = 4` → `[1, 2]`. Works fine, L and R start adjacent.
- **Negative numbers** `[-3, -1, 0, 2], target = -1` → two-pointer logic still holds since array is sorted.
- **Same element twice** `[1, 1], target = 2` → returns `[1, 2]`. L and R point to different indices.

---

## Common Mistakes

- Returning 0-indexed instead of 1-indexed — problem is 1-indexed, remember to add 1.
- Using a HashMap (valid but wastes O(n) space — the point of this problem is to use O(1) with two pointers).

---

## Related Problems

- **Two Sum (LC 1)** — unsorted, need HashMap O(n) space
- **3Sum (LC 15)** — fix one element, apply this exact pattern on the rest
- **4Sum (LC 18)** — two outer loops + this pattern
