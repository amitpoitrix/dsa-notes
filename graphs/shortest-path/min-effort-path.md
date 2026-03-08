# Path With Minimum Effort — LC #1631

**Pattern:** Dijkstra on Grid
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Find path from top-left to bottom-right minimizing the maximum absolute difference between consecutive cells.

---

## Code — Java

```java
public int minimumEffortPath(int[][] heights) {
    int m = heights.length, n = heights[0].length;
    int[][] effort = new int[m][n];
    for (int[] row : effort) Arrays.fill(row, Integer.MAX_VALUE);
    effort[0][0] = 0;

    PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[2]-b[2]);
    pq.offer(new int[]{0, 0, 0});
    int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};

    while (!pq.isEmpty()) {
        int[] curr = pq.poll();
        int r = curr[0], c = curr[1], e = curr[2];
        if (r == m-1 && c == n-1) return e;
        if (e > effort[r][c]) continue;
        for (int[] d : dirs) {
            int nr = r+d[0], nc = c+d[1];
            if (nr >= 0 && nr < m && nc >= 0 && nc < n) {
                int newEffort = Math.max(e, Math.abs(heights[nr][nc] - heights[r][c]));
                if (newEffort < effort[nr][nc]) {
                    effort[nr][nc] = newEffort;
                    pq.offer(new int[]{nr, nc, newEffort});
                }
            }
        }
    }
    return 0;
}
```

## Complexity — O(m*n * log(m*n)) time
