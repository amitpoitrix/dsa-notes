# Rotting Oranges — LC #994

**Pattern:** Multi-source BFS
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta

---

## Problem

Grid with fresh oranges (1), rotten (2), empty (0). Every minute, rotten oranges infect adjacent fresh ones. Return minutes until all fresh are rotten, or -1 if impossible.

---

## Intuition

Multi-source BFS starting from all rotten oranges simultaneously.

---

## Code — Java

```java
public int orangesRotting(int[][] grid) {
    int m = grid.length, n = grid[0].length;
    Queue<int[]> queue = new LinkedList<>();
    int fresh = 0;

    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++) {
            if (grid[i][j] == 2) queue.offer(new int[]{i, j});
            if (grid[i][j] == 1) fresh++;
        }

    if (fresh == 0) return 0;
    int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
    int minutes = 0;

    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            int[] cell = queue.poll();
            for (int[] d : dirs) {
                int r = cell[0] + d[0], c = cell[1] + d[1];
                if (r >= 0 && r < m && c >= 0 && c < n && grid[r][c] == 1) {
                    grid[r][c] = 2;
                    fresh--;
                    queue.offer(new int[]{r, c});
                }
            }
        }
        minutes++;
    }
    return fresh == 0 ? minutes - 1 : -1;
}
```

---

## Complexity — O(m*n) time and space
