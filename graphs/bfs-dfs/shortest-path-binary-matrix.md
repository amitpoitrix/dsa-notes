# Shortest Path in Binary Matrix — LC #1091

**Pattern:** BFS Shortest Path
**Difficulty:** Medium

---

## Problem

Find shortest clear path from top-left to bottom-right in binary matrix (8-directional, only through 0s).

---

## Code — Java

```java
public int shortestPathBinaryMatrix(int[][] grid) {
    int n = grid.length;
    if (grid[0][0] == 1 || grid[n-1][n-1] == 1) return -1;

    Queue<int[]> queue = new LinkedList<>();
    queue.offer(new int[]{0, 0, 1});
    grid[0][0] = 1;
    int[][] dirs = {{-1,-1},{-1,0},{-1,1},{0,-1},{0,1},{1,-1},{1,0},{1,1}};

    while (!queue.isEmpty()) {
        int[] curr = queue.poll();
        int r = curr[0], c = curr[1], dist = curr[2];
        if (r == n-1 && c == n-1) return dist;
        for (int[] d : dirs) {
            int nr = r+d[0], nc = c+d[1];
            if (nr >= 0 && nr < n && nc >= 0 && nc < n && grid[nr][nc] == 0) {
                queue.offer(new int[]{nr, nc, dist+1});
                grid[nr][nc] = 1;
            }
        }
    }
    return -1;
}
```

## Complexity — O(n²) time and space
