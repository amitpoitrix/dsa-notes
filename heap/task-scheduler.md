# Task Scheduler — LC #621

**Pattern:** Heap + Greedy
**Difficulty:** Medium
**Companies:** Facebook · Amazon · Microsoft

---

## Problem

Given tasks and cooldown `n`, find the minimum time to finish all tasks. Identical tasks must be separated by at least `n` intervals. You can insert idle intervals.

```
Input:  tasks = ["A","A","A","B","B","B"], n = 2
Output: 8   // A->B->idle->A->B->idle->A->B
```

---

## Intuition

Always pick the most frequent remaining task first — greedy. Use a max-heap by frequency. In each cycle of `n+1` slots, pick up to `n+1` most frequent tasks. If fewer than `n+1` tasks available, fill with idle time.

---

## Algorithm

1. Count task frequencies, push to max-heap.
2. While heap is not empty:
   - Process one cycle: pick up to `n+1` tasks from heap by frequency.
   - Decrease each picked task's count. If count > 0, push back.
   - Add `n+1` to time (or fewer if no more tasks remain after this cycle).
3. Return total time.

---

## Code — Java

```java
public int leastInterval(char[] tasks, int n) {
    int[] freq = new int[26];
    for (char t : tasks) freq[t - 'A']++;

    PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
    for (int f : freq) if (f > 0) maxHeap.offer(f);

    int time = 0;
    while (!maxHeap.isEmpty()) {
        List<Integer> temp = new ArrayList<>();
        int cycles = n + 1;

        while (cycles-- > 0 && !maxHeap.isEmpty()) {
            int f = maxHeap.poll();
            if (f > 1) temp.add(f - 1);
            time++;
        }

        maxHeap.addAll(temp);
        if (!maxHeap.isEmpty()) time += cycles + 1; // idle slots
    }
    return time;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n * t) | t = unique tasks, n = cooldown |
| Space | O(1) | At most 26 tasks in heap |

---

## Dry Run — ["A","A","A","B","B","B"], n=2

freq: A=3, B=3. Heap: [3,3]

| cycle | picked | heap after | time |
|-------|--------|------------|------|
| 1 | A(3→2), B(3→2) + idle | [2,2] | 3 |
| 2 | A(2→1), B(2→1) + idle | [1,1] | 6 |
| 3 | A(1→0), B(1→0) | [] | 8 |

**Result:** 8

---

## Edge Cases

- `n = 0` → no cooldown, answer = `tasks.length`.
- One unique task repeated — lots of idle time needed.

---

## Common Mistakes

- Adding idle time even on the last cycle — only add idle if heap still has remaining tasks after the cycle.

---

## Related Problems

- **Reorganize String (LC 767)** — same greedy heap, check if possible
- **Find Median from Data Stream (LC 295)** — heap design
