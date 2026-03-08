# Largest Rectangle in Histogram — LC #84

**Pattern:** Monotonic Increasing Stack
**Difficulty:** Hard
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Given array `heights` representing histogram bar heights, find the largest rectangle area.

```
Input:  heights = [2,1,5,6,2,3]
Output: 10   // width=2, height=5 (bars at index 2 and 3)
```

---

## Intuition

Use a monotonic increasing stack. When we see a bar shorter than the stack top, the stack-top bar can no longer extend right. Pop it and compute its maximum rectangle (height = popped bar, width = current index - new stack top - 1).

---

## Algorithm

1. Append 0 to heights (sentinel to flush stack at end).
2. Maintain increasing stack of indices.
3. When `heights[i] < heights[stack.top()]`:
   - Pop height `h`. Width = `i - stack.top() - 1` (or `i` if stack empty).
   - `area = h * width`. Update max.
4. Push `i`.

---

## Code — Java

```java
public int largestRectangleArea(int[] heights) {
    int[] h = Arrays.copyOf(heights, heights.length + 1); // add sentinel 0
    Deque<Integer> stack = new ArrayDeque<>();
    int maxArea = 0;

    for (int i = 0; i < h.length; i++) {
        while (!stack.isEmpty() && h[i] < h[stack.peek()]) {
            int height = h[stack.pop()];
            int width = stack.isEmpty() ? i : i - stack.peek() - 1;
            maxArea = Math.max(maxArea, height * width);
        }
        stack.push(i);
    }
    return maxArea;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each bar pushed and popped once |
| Space | O(n) | Stack |

---

## Dry Run — [2,1,5,6,2,3,0]

- i=0: push 0. stack=[0]
- i=1: h[1]=1 < h[0]=2. Pop 0, h=2, width=1, area=2. Stack empty so width=i=1. Push 1. stack=[1]
- i=2: 5>1, push. i=3: 6>5, push. stack=[1,2,3]
- i=4: h=2 < h[3]=6. Pop 3, h=6, width=4-2-1=1, area=6. Pop 2, h=5, width=4-1-1=2, area=10. 2>1 stop. Push 4.
- i=5: 3>2, push. stack=[1,4,5]
- i=6: sentinel 0 flushes all. Pop 5: h=3,w=6-4-1=1,area=3. Pop 4: h=2,w=6-1-1=4,area=8. Pop 1: h=1,w=6,area=6.

**Result:** 10

---

## Common Mistakes

- Width calculation: `i - stack.peek() - 1` (not `i - stack.peek()`).
- Not appending the 0 sentinel — stack never fully flushes without it.

---

## Related Problems

- **Maximal Rectangle (LC 85)** — apply this on each row of a matrix
- **Trapping Rain Water (LC 42)** — related bar-chart problem
