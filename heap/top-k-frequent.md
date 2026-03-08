# Top K Frequent Elements — LC #347

**Pattern:** Heap / Bucket Sort
**Difficulty:** Medium
**Companies:** Facebook · Amazon · Google · Uber

---

## Problem

Given array `nums` and integer `k`, return the `k` most frequent elements.

```
Input:  nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
```

---

## Intuition

Count frequencies with a HashMap. Then use a min-heap of size `k` to keep the top-k frequent elements. Min-heap root = least frequent among the top-k, so we evict it when we find something more frequent.

**Bucket sort alternative:** O(n) time. Since max frequency ≤ n, create bucket array of size n+1 where `bucket[freq]` = list of numbers with that frequency. Scan from high to low frequency to collect k elements.

---

## Algorithm (Heap approach)

1. Build frequency map.
2. Use min-heap keyed by frequency.
3. For each entry in freq map: add to heap, if `heap.size() > k` → poll.
4. Collect heap elements as result.

---

## Code — Java

```java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : nums) freq.merge(n, 1, Integer::sum);

    // min-heap by frequency
    PriorityQueue<Integer> heap = new PriorityQueue<>(
        (a, b) -> freq.get(a) - freq.get(b)
    );

    for (int num : freq.keySet()) {
        heap.offer(num);
        if (heap.size() > k) heap.poll();
    }

    int[] result = new int[k];
    for (int i = 0; i < k; i++) result[i] = heap.poll();
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log k) | n freq entries, heap ops O(log k) |
| Space | O(n) | Frequency map |

---

## Dry Run — [1,1,1,2,2,3], k=2

freq = {1:3, 2:2, 3:1}

| num | heap (by freq) | trim? |
|-----|----------------|-------|
| 1 (f=3) | [1] | — |
| 2 (f=2) | [2,1] | — |
| 3 (f=1) | [3,1,2] | poll 3 (f=1) → [2,1] |

**Result:** [2, 1] (order may vary)

---

## Edge Cases

- All elements same frequency — any k elements valid.
- `k == unique elements count` — return all.

---

## Common Mistakes

- Using max-heap and popping k times — works but no advantage over sorting. Min-heap of size k is the intended O(n log k) approach.
- Comparator: min-heap needs `freq.get(a) - freq.get(b)` (smaller frequency = higher priority to evict).

---

## Related Problems

- **Kth Largest Element (LC 215)** — heap on value
- **K Closest Points to Origin (LC 973)** — heap on distance
- **Sort Characters by Frequency (LC 451)** — sort by frequency
