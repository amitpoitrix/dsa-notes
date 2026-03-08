# Minimum Number of Arrows to Burst Balloons — LC #452

**Pattern:** Greedy (Sort by End)
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Balloons span `[xstart, xend]` on a number line. Arrows shot vertically burst all balloons the arrow passes through. Find minimum arrows to burst all balloons.

```
Input:  [[10,16],[2,8],[1,6],[7,12]]
Output: 2
```

---

## Intuition

Sort by end coordinate. Greedily shoot at the end of the first balloon. This bursts all overlapping balloons. Move to the next unbursted balloon and repeat.

---

## Code — Java

```java
public int findMinArrowShots(int[][] points) {
    Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));
    int arrows = 1, end = points[0][1];

    for (int i = 1; i < points.length; i++) {
        if (points[i][0] > end) { // balloon starts after current arrow
            arrows++;
            end = points[i][1];
        }
    }
    return arrows;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log n) | Sort |
| Space | O(1)       | |

---

## Key Difference from Non-overlapping Intervals

Here `[1,2]` and `[2,3]` DO share point 2 (one arrow bursts both). So use `>` not `>=` for the overlap check.

---

## Related Problems

- **Non-overlapping Intervals (LC 435)** — essentially the same greedy logic
