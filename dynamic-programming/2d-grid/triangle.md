# Triangle — LC #120

**Pattern:** 2D DP (Bottom-up)
**Difficulty:** Medium
**Companies:** Amazon · Microsoft

---

## Problem

Given a triangle array, find minimum path sum from top to bottom. Each step may move to adjacent numbers on the row below.

```
Input:  [[2],[3,4],[6,5,7],[4,1,8,3]]
Output: 11   // 2+3+5+1
```

---

## Intuition

Bottom-up DP. Start from second-last row. For each element, add the minimum of the two adjacent elements in the row below. After processing all rows, `triangle[0][0]` holds the answer.

---

## Code — Java

```java
public int minimumTotal(List<List<Integer>> triangle) {
    int n = triangle.size();
    int[] dp = new int[n];
    // init with last row
    for (int i = 0; i < n; i++) dp[i] = triangle.get(n-1).get(i);

    for (int row = n - 2; row >= 0; row--) {
        for (int col = 0; col <= row; col++) {
            dp[col] = triangle.get(row).get(col) + Math.min(dp[col], dp[col+1]);
        }
    }
    return dp[0];
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n²) |
| Space | O(n) |

---

## Related Problems

- **Minimum Path Sum (LC 64)** — same concept on rectangular grid
- **Dungeon Game (LC 174)** — reverse path DP
