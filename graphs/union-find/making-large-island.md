# Making a Large Island — LC #827

**Pattern:** Union-Find (DSU) on Grid
**Difficulty:** Hard
**Companies:** Google · Amazon

---

## Problem

Given an `n x n` binary grid, you may change at most one `0` to `1`. Return the size of the largest island after this change. An island is a group of connected 1s.

```
Input:  [[1,0],[0,1]]
Output: 3
```

---

## Intuition

Two-pass approach:
1. Use DSU to label each island and compute its size.
2. For each `0`, try flipping it to `1`. Sum up sizes of all unique adjacent islands + 1 (for the flipped cell itself). Track the maximum.

---

## Algorithm

1. Run DSU over all `1` cells, tracking component sizes.
2. Initialize `max = largest existing island` (in case no 0 exists).
3. For each `0` cell:
   - Collect unique roots of its 4 neighbors that are `1`.
   - Sum their sizes + 1.
   - Update `max`.
4. Return `max`.

---

## Code — Java

```java
int[] parent, size;

public int largestIsland(int[][] grid) {
    int n = grid.length;
    parent = new int[n * n];
    size = new int[n * n];
    for (int i = 0; i < n * n; i++) { parent[i] = i; size[i] = 1; }

    int[] dirs = {0,1,0,-1,1,0,-1,0};
    // pass 1: union all 1s
    for (int r = 0; r < n; r++) {
        for (int c = 0; c < n; c++) {
            if (grid[r][c] == 1) {
                for (int d = 0; d < 4; d++) {
                    int nr = r + dirs[d], nc = c + dirs[d+1];
                    if (nr >= 0 && nr < n && nc >= 0 && nc < n && grid[nr][nc] == 1)
                        union(r*n+c, nr*n+nc);
                }
            }
        }
    }

    // max island without flipping
    int max = 0;
    for (int i = 0; i < n*n; i++)
        if (grid[i/n][i%n] == 1) max = Math.max(max, size[find(i)]);

    // pass 2: try flipping each 0
    for (int r = 0; r < n; r++) {
        for (int c = 0; c < n; c++) {
            if (grid[r][c] == 0) {
                Set<Integer> seen = new HashSet<>();
                int total = 1;
                for (int d = 0; d < 4; d++) {
                    int nr = r + dirs[d], nc = c + dirs[d+1];
                    if (nr >= 0 && nr < n && nc >= 0 && nc < n && grid[nr][nc] == 1) {
                        int root = find(nr*n+nc);
                        if (seen.add(root)) total += size[root];
                    }
                }
                max = Math.max(max, total);
            }
        }
    }
    return max;
}

private int find(int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]);
    return parent[x];
}

private int find(int[] p, int x) {
    if (p[x] != x) p[x] = find(p, p[x]);
    return p[x];
}

private void union(int x, int y) {
    int px = find(x), py = find(y);
    if (px == py) return;
    if (size[px] < size[py]) { int t = px; px = py; py = t; }
    parent[py] = px;
    size[px] += size[py];
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n²) | Two passes over the grid |
| Space | O(n²) | DSU arrays |

---

## Edge Cases

- **All 1s** → no 0 to flip, return `n*n`.
- **All 0s** → flip one, return 1.
- **Single 0 surrounded by 1s** → merges all 4 neighbors + itself.

---

## Common Mistakes

- Not deduplicating neighbors by root — same island can appear multiple times in 4-directional scan.
- Not initializing `max` to largest existing island — if no 0 exists, the answer is the largest island.

---

## Related Problems

- **Number of Islands (LC 200)** — basic island counting
- **Max Area of Island (LC 695)** — find largest island without modification
