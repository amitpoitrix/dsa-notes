# Find Median from Data Stream — LC #295

**Pattern:** Two Heaps
**Difficulty:** Hard
**Companies:** Google · Amazon · Microsoft · Uber

---

## Problem

Design a data structure that supports adding integers and finding the median at any time.

```
MedianFinder mf = new MedianFinder();
mf.addNum(1);  mf.addNum(2);
mf.findMedian(); // 1.5
mf.addNum(3);
mf.findMedian(); // 2.0
```

---

## Intuition

Maintain two heaps:
- **Max-heap (small)** — holds the lower half of numbers. Root = max of lower half.
- **Min-heap (large)** — holds the upper half. Root = min of upper half.

Invariant: `small.size() == large.size()` or `small.size() == large.size() + 1`.

Median = `small.peek()` (odd total) or `(small.peek() + large.peek()) / 2.0` (even total).

---

## Algorithm

**addNum:**
1. Push to `small` (max-heap).
2. Balance: if `small.peek() > large.peek()` → move small's root to large.
3. Rebalance sizes: if `large.size() > small.size()` → move large's root to small.

**findMedian:**
- If sizes equal → `(small.peek() + large.peek()) / 2.0`
- Else → `small.peek()`

---

## Code — Java

```java
class MedianFinder {
    PriorityQueue<Integer> small; // max-heap (lower half)
    PriorityQueue<Integer> large; // min-heap (upper half)

    public MedianFinder() {
        small = new PriorityQueue<>(Collections.reverseOrder());
        large = new PriorityQueue<>();
    }

    public void addNum(int num) {
        small.offer(num);

        // ensure all of small <= all of large
        if (!large.isEmpty() && small.peek() > large.peek()) {
            large.offer(small.poll());
        }

        // balance sizes: small can have at most 1 more than large
        if (small.size() > large.size() + 1) {
            large.offer(small.poll());
        } else if (large.size() > small.size()) {
            small.offer(large.poll());
        }
    }

    public double findMedian() {
        if (small.size() == large.size()) {
            return (small.peek() + large.peek()) / 2.0;
        }
        return small.peek();
    }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| addNum  | O(log n) | Heap push/pop |
| findMedian | O(1) | Just peek at roots |
| Space | O(n) | All numbers stored |

---

## Dry Run — add 1, 2, 3

| op | small (max) | large (min) | median |
|----|-------------|-------------|--------|
| add(1) | [1] | [] | 1.0 |
| add(2) | [1] | [2] | 1.5 |
| add(3) | [2,1] | [3] | 2.0 |

---

## Edge Cases

- Single element → median = that element.
- All same elements → median = that element.

---

## Common Mistakes

- Forgetting to rebalance sizes after moving between heaps — invariant must hold after every addNum.
- Integer overflow when computing `(a + b) / 2.0` — cast to double before dividing.

---

## Related Problems

- **Sliding Window Median (LC 480)** — same two-heap idea + removal
- **IPO (LC 502)** — two heaps for greedy selection
