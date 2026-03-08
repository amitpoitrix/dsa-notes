# Two Sum — LC #1

**Pattern:** HashMap
**Difficulty:** Easy
**Companies:** Google · Amazon · Meta · Microsoft · Everywhere

---

## Problem

Given array `nums` and `target`, return indices of the two numbers that add up to `target`. Exactly one solution. Cannot use same element twice.

```
Input:  nums = [2, 7, 11, 15], target = 9
Output: [0, 1]   // nums[0] + nums[1] = 9
```

---

## Intuition

For each element, we need `target - nums[i]`. Check if that complement exists in a HashMap of previously seen numbers. If yes, return the pair. If no, store current number and its index.

---

## Algorithm

1. Create `HashMap<Integer, Integer>` (value → index).
2. For each `i`, compute `complement = target - nums[i]`.
3. If complement in map → return `[map.get(complement), i]`.
4. Else → `map.put(nums[i], i)`.

---

## Code — Java

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();

    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }
    return new int[]{};
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(n) | HashMap |

---

## Dry Run — [2, 7, 11, 15], target = 9

| i | nums[i] | complement | map             | result |
|---|---------|------------|-----------------|--------|
| 0 | 2       | 7          | {}→{2:0}        | —      |
| 1 | 7       | 2          | found 2 at idx 0| [0,1]  |

**Result:** [0, 1]

---

## Edge Cases

- Duplicate values: `[3, 3], target = 6` → works because we check before inserting.
- Negative numbers → works fine.

---

## Common Mistakes

- Inserting before checking → could match element with itself.
- Returning values instead of indices.

---

## Related Problems

- **Two Sum II (LC 167)** — sorted array, O(1) space with two pointers
- **3Sum (LC 15)** — three elements, sort + two pointer
- **4Sum (LC 18)** — four elements
