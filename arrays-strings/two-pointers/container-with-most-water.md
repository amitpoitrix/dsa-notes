# Container With Most Water — LC #11

**Pattern:** Two Pointers (Opposite Ends)
**Difficulty:** Medium
**Companies:** Google · Amazon · Microsoft · Bloomberg

---

## Problem

Given array `height` where `height[i]` is the height of a vertical line at index `i`, find two lines that together with the x-axis form a container that holds the most water. Return the max area.

```
Input:  height = [1, 8, 6, 2, 5, 4, 8, 3, 7]
Output: 49   // lines at index 1 (h=8) and index 8 (h=7), width=7, area = 7*7 = 49
```

---

## Intuition

Area = `min(height[L], height[R]) * (R - L)`.

Start with the widest container (L=0, R=n-1). To potentially increase area, we must increase the height — width can only shrink as we move pointers inward. So always move the pointer with the **shorter height** inward. Moving the taller one can never increase area (width shrinks, height bounded by the shorter side anyway).

---

## Algorithm

1. Set `L = 0`, `R = n - 1`, `maxArea = 0`.
2. While `L < R`:
   - Compute `area = min(height[L], height[R]) * (R - L)`.
   - Update `maxArea`.
   - Move the pointer with the shorter height inward:
     - `height[L] < height[R]` → `L++`
     - else → `R--`
3. Return `maxArea`.

---

## Code — Java

```java
public int maxArea(int[] height) {
    int L = 0, R = height.length - 1;
    int maxArea = 0;

    while (L < R) {
        int area = Math.min(height[L], height[R]) * (R - L);
        maxArea = Math.max(maxArea, area);

        if (height[L] < height[R]) {
            L++;
        } else {
            R--;
        }
    }
    return maxArea;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass, each pointer moves at most n times |
| Space | O(1) | No extra data structures |

---

## Dry Run — [1, 8, 6, 2, 5, 4, 8, 3, 7]

| L | R | h[L] | h[R] | area | maxArea | Action |
|---|---|------|------|------|---------|--------|
| 0 | 8 | 1    | 7    | 8    | 8       | L++ (1 < 7) |
| 1 | 8 | 8    | 7    | 49   | 49      | R-- (8 >= 7) |
| 1 | 7 | 8    | 3    | 18   | 49      | R-- (8 >= 3) |
| 1 | 6 | 8    | 8    | 40   | 49      | R-- (tie) |
| 1 | 5 | 8    | 4    | 32   | 49      | R-- |
| 1 | 4 | 8    | 5    | 15   | 49      | R-- |
| 1 | 3 | 8    | 2    | 16   | 49      | R-- |
| 1 | 2 | 8    | 6    | 6    | 49      | R-- |
| 1 | 1 | —    | —    | —    | —       | L == R, stop |

**Result:** 49

---

## Edge Cases

- **Two elements** `[1, 1]` → area = 1. Works fine.
- **All same heights** `[5, 5, 5, 5]` → always moves R--, still finds max.
- **Increasing heights** `[1, 2, 3, 4]` → correctly moves L pointer up.

---

## Common Mistakes

- Moving the taller pointer instead of the shorter one — this is the core greedy insight, easy to get backwards.
- Computing width as `R - L + 1` instead of `R - L` — the container width is the gap between indices, not the count.

---

## Related Problems

- **Trapping Rain Water (LC 42)** — harder variant, water trapped between all bars
- **Two Sum II (LC 167)** — same opposite-pointer setup
- **3Sum (LC 15)** — sort + two pointers
