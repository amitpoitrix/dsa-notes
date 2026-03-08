# Is Graph Bipartite? — LC #785

**Pattern:** BFS 2-Coloring
**Difficulty:** Medium
**Companies:** Google · Meta

---

## Problem

A graph is bipartite if nodes can be split into two groups where no two nodes in the same group are adjacent.

---

## Code — Java (BFS)

```java
public boolean isBipartite(int[][] graph) {
    int[] color = new int[graph.length]; // 0=uncolored, 1/-1=two colors

    for (int i = 0; i < graph.length; i++) {
        if (color[i] != 0) continue;
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(i); color[i] = 1;
        while (!queue.isEmpty()) {
            int node = queue.poll();
            for (int neighbor : graph[node]) {
                if (color[neighbor] == 0) { color[neighbor] = -color[node]; queue.offer(neighbor); }
                else if (color[neighbor] == color[node]) return false;
            }
        }
    }
    return true;
}
```

## Complexity — O(n + e) time and space
