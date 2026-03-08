# Critical Connections in Network — LC #1192

**Pattern:** Tarjan's Bridge Finding
**Difficulty:** Hard
**Companies:** Amazon · Uber · Google

---

## Problem

Find all critical connections (bridges) — edges whose removal disconnects the network.

---

## Intuition

Use Tarjan's algorithm. Track discovery time and low value (earliest ancestor reachable). An edge (u, v) is a bridge if `low[v] > disc[u]` (v cannot reach u or earlier via any other path).

---

## Code — Java

```java
int timer = 0;

public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) {
    List<List<Integer>> adj = new ArrayList<>();
    for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
    for (List<Integer> c : connections) { adj.get(c.get(0)).add(c.get(1)); adj.get(c.get(1)).add(c.get(0)); }

    int[] disc = new int[n], low = new int[n];
    Arrays.fill(disc, -1);
    List<List<Integer>> result = new ArrayList<>();
    dfs(adj, disc, low, result, 0, -1);
    return result;
}

private void dfs(List<List<Integer>> adj, int[] disc, int[] low, List<List<Integer>> res, int u, int parent) {
    disc[u] = low[u] = timer++;
    for (int v : adj.get(u)) {
        if (v == parent) continue;
        if (disc[v] == -1) {
            dfs(adj, disc, low, res, v, u);
            low[u] = Math.min(low[u], low[v]);
            if (low[v] > disc[u]) res.add(Arrays.asList(u, v)); // bridge
        } else {
            low[u] = Math.min(low[u], disc[v]);
        }
    }
}
```

## Complexity — O(V + E) time and space
