# Redundant Connection — LC #684

**Pattern:** Union-Find (DSU)
**Difficulty:** Medium
**Companies:** Amazon · Google · Facebook

---

## Problem

Given a graph that started as a tree with `n` nodes and one extra edge added, find and return that redundant edge. If multiple answers exist, return the one that appears last in the input.

```
Input:  edges = [[1,2],[1,3],[2,3]]
Output: [2,3]
```

---

## Intuition

Use Union-Find. Process edges one by one. For each edge `[u, v]`, check if `u` and `v` are already connected (same component). If yes — this edge creates a cycle, it's the redundant one. If no — union them.

---

## Algorithm

1. Initialize `parent[i] = i` for all nodes.
2. For each edge `[u, v]`:
   - `find(u) == find(v)` → return this edge (redundant).
   - Else → `union(u, v)`.
3. Never reached if input is valid.

---

## Code — Java

```java
public int[] findRedundantConnection(int[][] edges) {
    int n = edges.length;
    int[] parent = new int[n + 1];
    int[] rank = new int[n + 1];
    for (int i = 0; i <= n; i++) parent[i] = i;

    for (int[] edge : edges) {
        if (find(parent, edge[0]) == find(parent, edge[1])) {
            return edge;
        }
        union(parent, rank, edge[0], edge[1]);
    }
    return new int[]{};
}

private int find(int[] parent, int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]); // path compression
    return parent[x];
}

private void union(int[] parent, int[] rank, int x, int y) {
    int px = find(parent, x), py = find(parent, y);
    if (rank[px] > rank[py]) parent[py] = px;
    else if (rank[px] < rank[py]) parent[px] = py;
    else { parent[py] = px; rank[px]++; }
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n α(n)) | α is inverse Ackermann, nearly O(1) per operation |
| Space | O(n) | parent and rank arrays |

---

## Dry Run — [[1,2],[1,3],[2,3]]

| Edge | find(1) | find(2/3) | Same? | Action |
|------|---------|-----------|-------|--------|
| [1,2] | 1 | 2 | No | union(1,2) |
| [1,3] | 1 | 3 | No | union(1,3) |
| [2,3] | 1 | 1 | Yes ✓ | return [2,3] |

---

## Edge Cases

- Graph guaranteed to have exactly one redundant edge per problem constraints.
- Return last redundant edge if multiple exist — processing order handles this.

---

## Common Mistakes

- Forgetting path compression in `find` — still correct but O(log n) per op instead of near O(1).
- Using 0-indexed when nodes are 1-indexed — initialize `parent` of size `n+1`.

---

## Related Problems

- **Graph Valid Tree (LC 261)** — union-find to check no cycle + connected
- **Number of Connected Components (LC 323)** — basic DSU application
- **Accounts Merge (LC 721)** — DSU on strings
