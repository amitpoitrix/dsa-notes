# Number of Connected Components — LC #323

**Pattern:** DFS / Union-Find
**Difficulty:** Medium

---

## Code — Java (DFS on adjacency list)

```java
public int countComponents(int n, int[][] edges) {
    List<List<Integer>> adj = new ArrayList<>();
    for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
    for (int[] e : edges) { adj.get(e[0]).add(e[1]); adj.get(e[1]).add(e[0]); }

    boolean[] visited = new boolean[n];
    int count = 0;
    for (int i = 0; i < n; i++) {
        if (!visited[i]) { dfs(adj, visited, i); count++; }
    }
    return count;
}

private void dfs(List<List<Integer>> adj, boolean[] visited, int node) {
    visited[node] = true;
    for (int neighbor : adj.get(node)) if (!visited[neighbor]) dfs(adj, visited, neighbor);
}
```

## Complexity — O(n + e) time and space
