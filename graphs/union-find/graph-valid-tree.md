# Graph Valid Tree — LC #261

**Pattern:** Union-Find (DSU)
**Difficulty:** Medium
**Companies:** Google · LinkedIn · Snap

---

## Problem

Given `n` nodes (0 to n-1) and a list of edges, return `true` if the edges form a valid tree.

```
Input:  n = 5, edges = [[0,1],[0,2],[0,3],[1,4]]
Output: true

Input:  n = 5, edges = [[0,1],[1,2],[2,3],[1,3],[1,4]]
Output: false
```

---

## Intuition

A valid tree has exactly two properties:
1. **No cycle** — exactly `n-1` edges.
2. **Fully connected** — all nodes in one component.

Use Union-Find. If we try to union two nodes already in the same component → cycle detected → not a tree. After processing all edges, check that exactly one component exists.

---

## Algorithm

1. If `edges.length != n - 1` → return false immediately.
2. Initialize DSU for `n` nodes.
3. For each edge `[u, v]`:
   - If `find(u) == find(v)` → cycle → return false.
   - Else union them.
4. Return true (edge count check already guarantees connectivity).

---

## Code — Java

```java
public boolean validTree(int n, int[][] edges) {
    if (edges.length != n - 1) return false;

    int[] parent = new int[n];
    for (int i = 0; i < n; i++) parent[i] = i;

    for (int[] edge : edges) {
        int p1 = find(parent, edge[0]);
        int p2 = find(parent, edge[1]);
        if (p1 == p2) return false; // cycle
        parent[p1] = p2;
    }
    return true;
}

private int find(int[] parent, int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]);
    return parent[x];
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n α(n)) | Near linear with path compression |
| Space | O(n) | Parent array |

---

## Dry Run — n=5, [[0,1],[0,2],[0,3],[1,4]]

edges.length = 4 = n-1 = 4 ✓

| Edge | find(u) | find(v) | Same? | Action |
|------|---------|---------|-------|--------|
| [0,1] | 0 | 1 | No | union |
| [0,2] | 0 | 2 | No | union |
| [0,3] | 0 | 3 | No | union |
| [1,4] | 0 | 4 | No | union |

No cycle found → **true**

---

## Edge Cases

- `n=1, edges=[]` → true (single node, no edges needed).
- Disconnected graph with n-1 edges — impossible if no cycles since n-1 edges + n nodes + connected = tree. Edge count check handles this.

---

## Common Mistakes

- Not checking `edges.length != n-1` upfront — saves time and handles disconnected graphs.
- Forgetting that a tree must be both acyclic AND connected.

---

## Related Problems

- **Redundant Connection (LC 684)** — find the extra edge that causes a cycle
- **Number of Connected Components (LC 323)** — count components with DSU
- **Course Schedule (LC 207)** — cycle detection in directed graph
