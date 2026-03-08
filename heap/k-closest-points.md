# K Closest Points to Origin — LC #973

**Pattern:** Heap (Max-Heap of size K)
**Difficulty:** Medium
**Companies:** Facebook · Amazon · LinkedIn

---

## Problem

Given array of `points` on a plane, return the `k` closest to the origin `(0,0)`. Distance is Euclidean: `sqrt(x²+y²)`. No need to sort the answer.

```
Input:  points = [[1,3],[-2,2]], k = 1
Output: [[-2,2]]   // dist=√8 < dist=√10
```

---

## Intuition

Use a max-heap of size `k` keyed by distance. The root is always the farthest among the k closest seen so far. When a closer point arrives, it evicts the current farthest. No need to take `sqrt` — compare `x²+y²` directly.

---

## Algorithm

1. Use max-heap (negate distance to simulate with Java's min-heap).
2. For each point: add to heap, if `size > k` → poll (removes farthest).
3. Collect remaining heap elements as result.

---

## Code — Java

```java
public int[][] kClosest(int[][] points, int k) {
    // max-heap by distance squared
    PriorityQueue<int[]> maxHeap = new PriorityQueue<>(
        (a, b) -> (b[0]*b[0] + b[1]*b[1]) - (a[0]*a[0] + a[1]*a[1])
    );

    for (int[] point : points) {
        maxHeap.offer(point);
        if (maxHeap.size() > k) maxHeap.poll(); // remove farthest
    }

    int[][] result = new int[k][2];
    for (int i = 0; i < k; i++) result[i] = maxHeap.poll();
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log k) | n points, each heap op O(log k) |
| Space | O(k) | Heap holds k points |

---

## Edge Cases

- `k == points.length` → return all points.
- Points at same distance — any valid subset acceptable.

---

## Common Mistakes

- Taking `sqrt` in comparison — unnecessary and slower. Compare squared distances directly.
- Using min-heap and popping k times — O(n log n) overall, loses the O(n log k) advantage.

---

## Related Problems

- **Kth Largest Element (LC 215)** — same heap pattern on values
- **Top K Frequent Elements (LC 347)** — heap on frequency
- **Find Median from Data Stream (LC 295)** — two heaps
