# Trapping Rain Water — LC #42

**Pattern:** Two Pointers (Opposite Ends)
**Difficulty:** Hard
**Companies:** Google · Amazon · Meta · Microsoft · Uber

---

## Problem

Given array `height` representing an elevation map, compute how much water it can trap after raining.

```
Input:  height = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]
Output: 6
```

---

## Intuition

Water above any bar `i` = `min(maxLeft, maxRight) - height[i]`.

Brute force precomputes `maxLeft[i]` and `maxRight[i]` arrays → O(n) time, O(n) space.

**Two-pointer optimization:** We don't need both arrays at once. If `maxLeft < maxRight`, the water at `L` is determined entirely by `maxLeft` (we know right side is taller). So process `L` and move it inward. Otherwise process `R`. This gives O(1) space.

---

## Algorithm

1. Set `L = 0`, `R = n-1`, `maxLeft = 0`, `maxRight = 0`, `water = 0`.
2. While `L < R`:
   - If `height[L] <= height[R]`:
     - If `height[L] >= maxLeft` → update `maxLeft`.
     - Else → `water += maxLeft - height[L]`.
     - `L++`.
   - Else:
     - If `height[R] >= maxRight` → update `maxRight`.
     - Else → `water += maxRight - height[R]`.
     - `R--`.
3. Return `water`.

---

## Code — Java

```java
public int trap(int[] height) {
    int L = 0, R = height.length - 1;
    int maxLeft = 0, maxRight = 0;
    int water = 0;

    while (L < R) {
        if (height[L] <= height[R]) {
            if (height[L] >= maxLeft) {
                maxLeft = height[L];    // update max, no water here
            } else {
                water += maxLeft - height[L];
            }
            L++;
        } else {
            if (height[R] >= maxRight) {
                maxRight = height[R];   // update max, no water here
            } else {
                water += maxRight - height[R];
            }
            R--;
        }
    }
    return water;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass with two pointers |
| Space | O(1) | Only four integer variables |

---

## Dry Run — [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]

| L | R | h[L] | h[R] | maxL | maxR | water | Action |
|---|---|------|------|------|------|-------|--------|
| 0 | 11 | 0 | 1 | 0 | 0 | 0 | maxL=0, L++ |
| 1 | 11 | 1 | 1 | 1 | 0 | 0 | maxL=1, L++ |
| 2 | 11 | 0 | 1 | 1 | 0 | 1 | water+=1, L++ |
| 3 | 11 | 2 | 1 | 2 | 0 | 1 | h[L]>h[R], maxR=1, R-- |
| 3 | 10 | 2 | 2 | 2 | 2 | 1 | h[L]<=h[R], maxL=2, L++ |
| ... | ... | ... | ... | ... | ... | ... | (continues to 6) |

**Result:** 6

---

## Edge Cases

- **Flat array** `[3, 3, 3]` → no water trapped, returns 0.
- **Strictly increasing** `[1, 2, 3]` → no water trapped, returns 0.
- **V-shape** `[3, 0, 3]` → 3 units trapped.
- **Single bar** `[5]` → 0.

---

## Common Mistakes

- Forgetting to update `maxLeft`/`maxRight` before computing water — if current bar is taller than max, it becomes the new wall, no water added.
- Using `height[L] < height[R]` (strict) vs `<=` — either works but be consistent with which pointer you move on a tie.

---

## Related Problems

- **Container With Most Water (LC 11)** — simpler variant, just two walls
- **Largest Rectangle in Histogram (LC 84)** — related bar-chart problem
- **Product of Array Except Self (LC 238)** — similar left/right traversal idea
