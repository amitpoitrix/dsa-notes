# Range Sum Query (Immutable) — LC #303

**Pattern:** Prefix Sum
**Difficulty:** Easy
**Companies:** Amazon · Microsoft

---

## Problem

Given array `nums`, handle multiple `sumRange(left, right)` queries returning the sum between indices `left` and `right` inclusive.

```
Input:  nums = [-2, 0, 3, -5, 2, -1]
        sumRange(0, 2) → 1
        sumRange(2, 5) → -1
```

---

## Intuition

Precompute prefix sums. `sumRange(l, r) = prefix[r+1] - prefix[l]`.

---

## Code — Java

```java
class NumArray {
    private int[] prefix;

    public NumArray(int[] nums) {
        prefix = new int[nums.length + 1];
        for (int i = 0; i < nums.length; i++) {
            prefix[i + 1] = prefix[i] + nums[i];
        }
    }

    public int sumRange(int left, int right) {
        return prefix[right + 1] - prefix[left];
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Build | O(n) | One pass |
| Query | O(1) | Direct subtraction |
| Space | O(n) | Prefix array |

---

## Common Mistakes

- Off-by-one: `prefix` has size `n+1`, `prefix[0] = 0`.

---

---

# Contiguous Array — LC #525

**Pattern:** Prefix Sum + HashMap
**Difficulty:** Medium
**Companies:** Meta · Amazon

---

## Problem

Given binary array `nums`, find the maximum length subarray with equal number of 0s and 1s.

```
Input:  [0, 1, 0]
Output: 2   // [0, 1] or [1, 0]
```

---

## Intuition

Replace 0s with -1. Now problem becomes: longest subarray with sum = 0. Use prefix sum + HashMap. If same prefix sum appears twice, the subarray between those indices sums to 0.

---

## Code — Java

```java
public int findMaxLength(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, -1); // sum 0 seen at index -1

    int sum = 0, maxLen = 0;

    for (int i = 0; i < nums.length; i++) {
        sum += (nums[i] == 0) ? -1 : 1;

        if (map.containsKey(sum)) {
            maxLen = Math.max(maxLen, i - map.get(sum));
        } else {
            map.put(sum, i); // only store first occurrence
        }
    }
    return maxLen;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass |
| Space | O(n) | HashMap |

---

## Dry Run — [0, 1, 0]

| i | nums[i] | sum | map | maxLen |
|---|---------|-----|-----|--------|
| — | —       | 0   | {0:-1} | 0   |
| 0 | 0       | -1  | {0:-1,-1:0} | 0 |
| 1 | 1       | 0   | seen at -1 → len=2 | 2 |
| 2 | 0       | -1  | seen at 0 → len=2 | 2 |

**Result:** 2

---

## Common Mistakes

- Storing sum at every index instead of just the first — you want maximum length, so keep the earliest index.
- Initializing `map.put(0, -1)` not `map.put(0, 0)` — the base case is before index 0.

---

---

# Minimum Size Subarray Sum — LC #209

**Pattern:** Sliding Window (Variable)
**Difficulty:** Medium
**Companies:** Amazon · Microsoft

---

## Problem

Given array `nums` and target `target`, find the minimum length subarray whose sum >= target. Return 0 if none.

```
Input:  target = 7, nums = [2,3,1,2,4,3]
Output: 2   // [4,3]
```

---

## Code — Java

```java
public int minSubArrayLen(int target, int[] nums) {
    int L = 0, sum = 0, minLen = Integer.MAX_VALUE;

    for (int R = 0; R < nums.length; R++) {
        sum += nums[R];
        while (sum >= target) {
            minLen = Math.min(minLen, R - L + 1);
            sum -= nums[L++];
        }
    }
    return minLen == Integer.MAX_VALUE ? 0 : minLen;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each element added/removed once |
| Space | O(1) | Only counters |

---

## Common Mistakes

- Returning -1 instead of 0 when no valid subarray found.
- Using `sum == target` instead of `sum >= target`.
