# Pacific Atlantic Water Flow — LC #417

**Pattern:** Reverse Multi-source BFS/DFS
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Water flows from high to low. Find cells that can reach both Pacific (top/left) and Atlantic (bottom/right).

---

## Intuition

Reverse the problem: do BFS/DFS from Pacific borders uphill. Do same from Atlantic borders. Cells reachable from both are the answer.

---

## Code — Java

```java
public List<List<Integer>> pacificAtlantic(int[][] heights) {
    int m = heights.length, n = heights[0].length;
    boolean[][] pac = new boolean[m][n], atl = new boolean[m][n];

    Queue<int[]> pQ = new LinkedList<>(), aQ = new LinkedList<>();
    for (int i = 0; i < m; i++) {
        pQ.offer(new int[]{i, 0}); pac[i][0] = true;
        aQ.offer(new int[]{i, n-1}); atl[i][n-1] = true;
    }
    for (int j = 0; j < n; j++) {
        pQ.offer(new int[]{0, j}); pac[0][j] = true;
        aQ.offer(new int[]{m-1, j}); atl[m-1][j] = true;
    }

    bfs(pQ, pac, heights); bfs(aQ, atl, heights);

    List<List<Integer>> result = new ArrayList<>();
    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            if (pac[i][j] && atl[i][j]) result.add(Arrays.asList(i, j));
    return result;
}

private void bfs(Queue<int[]> q, boolean[][] visited, int[][] h) {
    int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
    while (!q.isEmpty()) {
        int[] cell = q.poll();
        for (int[] d : dirs) {
            int r = cell[0]+d[0], c = cell[1]+d[1];
            if (r >= 0 && r < h.length && c >= 0 && c < h[0].length
                && !visited[r][c] && h[r][c] >= h[cell[0]][cell[1]]) {
                visited[r][c] = true;
                q.offer(new int[]{r, c});
            }
        }
    }
}
```

---

## Complexity — O(m*n) time and space
