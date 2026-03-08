# Top K Frequent Elements — LC #347

**Pattern:** HashMap + Bucket Sort (or Heap)
**Difficulty:** Medium
**Companies:** Amazon · Meta · Google · Microsoft

---

## Problem

Given array `nums` and integer `k`, return the `k` most frequent elements.

```
Input:  nums = [1,1,1,2,2,3], k = 2
Output: [1, 2]
```

---

## Intuition

**Bucket Sort approach (O(n)):** Count frequencies. Use index as frequency, bucket[freq] = list of numbers with that freq. Iterate buckets from high freq to low, collect until k elements found.

**Heap approach (O(n log k)):** Count frequencies. Use min-heap of size k. Simpler to code, slightly worse complexity.

---

## Code — Java (Bucket Sort)

```java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : nums) freq.put(n, freq.getOrDefault(n, 0) + 1);

    // bucket[i] = list of numbers with frequency i
    List<Integer>[] bucket = new List[nums.length + 1];
    for (int num : freq.keySet()) {
        int f = freq.get(num);
        if (bucket[f] == null) bucket[f] = new ArrayList<>();
        bucket[f].add(num);
    }

    int[] result = new int[k];
    int idx = 0;
    for (int f = bucket.length - 1; f >= 0 && idx < k; f--) {
        if (bucket[f] != null) {
            for (int num : bucket[f]) {
                result[idx++] = num;
                if (idx == k) break;
            }
        }
    }
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Bucket sort is O(n) |
| Space | O(n) | Frequency map + buckets |

---

## Common Mistakes

- Using max-heap of all elements → O(n log n), defeats the purpose.
- Bucket size: must be `nums.length + 1` (max frequency can be n).

---

## Related Problems

- **Top K Frequent Words (LC 692)** — same but with strings and lexicographic tiebreak
- **Kth Largest Element (LC 215)** — single element, use quickselect or heap
