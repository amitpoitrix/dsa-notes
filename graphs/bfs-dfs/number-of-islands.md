# Number of Islands — LC #200

**Pattern:** DFS/BFS Flood Fill
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta · Microsoft · Uber

---

## Problem

Given 2D grid of '1's and '0's, count number of islands (connected group of '1's).

```
Input:  [["1","1","0"],["1","1","0"],["0","0","1"]]
Output: 2
```

---

## Intuition

For each unvisited '1', run DFS/BFS to mark all connected land as visited. Count how many times we start a new DFS.

---

## Code — Java (DFS)

```java
public int numIslands(char[][] grid) {
    int count = 0;
    for (int i = 0; i < grid.length; i++) {
        for (int j = 0; j < grid[0].length; j++) {
            if (grid[i][j] == '1') {
                dfs(grid, i, j);
                count++;
            }
        }
    }
    return count;
}

private void dfs(char[][] grid, int i, int j) {
    if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] != '1') return;
    grid[i][j] = '0'; // mark visited
    dfs(grid, i+1, j); dfs(grid, i-1, j);
    dfs(grid, i, j+1); dfs(grid, i, j-1);
}
```

---

## Complexity — O(m*n) time and space
