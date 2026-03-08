# Reorganize String — LC #767

**Pattern:** Heap + Greedy
**Difficulty:** Medium
**Companies:** Amazon · Google · Facebook

---

## Problem

Given string `s`, rearrange characters so no two adjacent characters are the same. Return any valid arrangement, or empty string if impossible.

```
Input:  s = "aab"
Output: "aba"

Input:  s = "aaab"
Output: ""   // impossible
```

---

## Intuition

Greedy: always place the most frequent remaining character — as long as it's different from the last placed. Use a max-heap. After placing a character, hold it back for one step (can't use consecutively), then return it to the heap.

**Impossible check:** if max frequency > `(n+1)/2`, it's impossible.

---

## Algorithm

1. Count frequencies, push to max-heap.
2. While heap is not empty:
   - Pop most frequent `(count1, char1)`.
   - Append `char1` to result.
   - If there's a previously held-back character, push it back.
   - Hold `char1` (with decremented count) for next iteration.
3. If held-back remains at the end → impossible, return `""`.

---

## Code — Java

```java
public String reorganizeString(String s) {
    int[] freq = new int[26];
    for (char c : s.toCharArray()) freq[c - 'a']++;

    PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> b[0] - a[0]);
    for (int i = 0; i < 26; i++) {
        if (freq[i] > 0) maxHeap.offer(new int[]{freq[i], i});
    }

    StringBuilder sb = new StringBuilder();
    int[] prev = null;

    while (!maxHeap.isEmpty()) {
        int[] curr = maxHeap.poll();
        sb.append((char)('a' + curr[1]));
        if (prev != null && prev[0] > 0) maxHeap.offer(prev);
        curr[0]--;
        prev = curr;
    }

    return sb.length() == s.length() ? sb.toString() : "";
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log 26) = O(n) | n chars, heap size ≤ 26 |
| Space | O(n) | Result string |

---

## Edge Cases

- Single character `"a"` → return `"a"`.
- `"aa"` → impossible, return `""`.
- All same character → impossible unless length 1.

---

## Common Mistakes

- Not checking impossibility — if any char has freq > (n+1)/2 it can never be spaced out.
- Pushing back the held character too early — must hold it for exactly one step.

---

## Related Problems

- **Task Scheduler (LC 621)** — same greedy idea with idle slots
- **Rearrange String k Distance Apart (LC 358)** — generalization with distance k
