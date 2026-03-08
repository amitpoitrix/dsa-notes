# Kth Largest Element in Array — LC #215

**Pattern:** Heap (Min-Heap of size K)
**Difficulty:** Medium
**Companies:** Facebook · Amazon · Google · Microsoft

---

## Problem

Find the `k`th largest element in an unsorted array. Not the `k`th distinct element.

```
Input:  nums = [3,2,1,5,6,4], k = 2
Output: 5
```

---

## Intuition

Maintain a min-heap of size `k`. The root is always the smallest of the k largest elements seen so far — which is the kth largest overall. For each element: push it in, then if heap size > k, pop the smallest. At the end, heap root = kth largest.

---

## Algorithm

1. Create a min-heap (PriorityQueue in Java).
2. For each number in `nums`:
   - Add to heap.
   - If `heap.size() > k` → poll (remove smallest).
3. Return `heap.peek()`.

---

## Code — Java

```java
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> minHeap = new PriorityQueue<>();

    for (int num : nums) {
        minHeap.offer(num);
        if (minHeap.size() > k) {
            minHeap.poll(); // remove smallest
        }
    }
    return minHeap.peek(); // kth largest
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log k) | n insertions, each O(log k) |
| Space | O(k) | Heap holds at most k elements |

---

## Dry Run — [3,2,1,5,6,4], k=2

| num | heap after add | heap after trim | heap |
|-----|----------------|-----------------|------|
| 3   | [3]            | —               | [3] |
| 2   | [2,3]          | —               | [2,3] |
| 1   | [1,3,2]        | pop 1           | [2,3] |
| 5   | [2,3,5]        | pop 2           | [3,5] |
| 6   | [3,5,6]        | pop 3           | [5,6] |
| 4   | [4,5,6]        | pop 4           | [5,6] |

**peek = 5** ✓

---

## Edge Cases

- `k == 1` → return maximum element.
- `k == nums.length` → return minimum element.
- Duplicates — works fine, heap handles duplicates naturally.

---

## Common Mistakes

- Using a max-heap and collecting k elements — correct but O(n log n), more complex.
- Returning `heap.poll()` instead of `heap.peek()` — modifies the heap unnecessarily.

---

## Variants

- **Kth Smallest** → use a max-heap of size k instead. Keep k smallest → root is kth smallest.

---

## Related Problems

- **Top K Frequent Elements (LC 347)** — heap on frequency
- **K Closest Points to Origin (LC 973)** — heap on distance
- **Find Median from Data Stream (LC 295)** — two heaps
