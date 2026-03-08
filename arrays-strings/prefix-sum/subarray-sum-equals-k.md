# Subarray Sum Equals K — LC #560

**Pattern:** Prefix Sum + HashMap
**Difficulty:** Medium
**Companies:** Google · Meta · Amazon · Microsoft

---

## Problem

Given array `nums` and integer `k`, return the total number of subarrays whose sum equals `k`.

```
Input:  nums = [1, 1, 1], k = 2
Output: 2   // [1,1] at index 0-1 and index 1-2
```

---

## Intuition

`sum(i..j) = prefixSum[j] - prefixSum[i-1]`. So we need `prefixSum[j] - prefixSum[i-1] == k`, which means `prefixSum[i-1] == prefixSum[j] - k`.

As we build prefix sum, store counts in a HashMap. For each new prefix sum, check if `(currentSum - k)` exists in the map.

---

## Algorithm

1. Initialize `map = {0: 1}` (empty prefix has sum 0, seen once).
2. Set `sum = 0`, `count = 0`.
3. Loop through `nums`:
   - `sum += nums[i]`.
   - If `map.containsKey(sum - k)` → `count += map.get(sum - k)`.
   - `map.put(sum, map.getOrDefault(sum, 0) + 1)`.
4. Return `count`.

---

## Code — Java

```java
public int subarraySum(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, 1); // empty prefix

    int sum = 0, count = 0;

    for (int num : nums) {
        sum += num;
        count += map.getOrDefault(sum - k, 0);
        map.put(sum, map.getOrDefault(sum, 0) + 1);
    }
    return count;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(n) | Map stores all prefix sums |

---

## Dry Run — [1, 1, 1], k = 2

| i | num | sum | sum-k | map.get(sum-k) | count | map |
|---|-----|-----|-------|----------------|-------|-----|
| — | —   | 0   | —     | —              | 0     | {0:1} |
| 0 | 1   | 1   | -1    | 0              | 0     | {0:1, 1:1} |
| 1 | 1   | 2   | 0     | 1              | 1     | {0:1,1:1,2:1} |
| 2 | 1   | 3   | 1     | 1              | 2     | {0:1,1:1,2:1,3:1} |

**Result:** 2

---

## Edge Cases

- Negative numbers → still works, HashMap handles any integer prefix sums.
- `k = 0` → counts subarrays that sum to 0, `map.put(0,1)` initialization is critical here.

---

## Common Mistakes

- Forgetting `map.put(0, 1)` — misses subarrays starting from index 0.
- Using a sliding window instead — doesn't work with negative numbers.

---

## Related Problems

- **Contiguous Array (LC 525)** — same technique, equal 0s and 1s
- **Product of Array Except Self (LC 238)** — prefix product variant
- **Path Sum III (LC 437)** — same prefix sum + hashmap on a tree
