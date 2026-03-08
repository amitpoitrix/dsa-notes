# Find the City With Smallest Neighbors — LC #1334

**Pattern:** Floyd-Warshall
**Difficulty:** Medium

---

## Problem

Find the city with the smallest number of reachable cities within threshold distance. Tie → largest index.

---

## Code — Java

```java
public int findTheCity(int n, int[][] edges, int distanceThreshold) {
    int[][] dist = new int[n][n];
    for (int[] row : dist) Arrays.fill(row, Integer.MAX_VALUE / 2);
    for (int i = 0; i < n; i++) dist[i][i] = 0;
    for (int[] e : edges) { dist[e[0]][e[1]] = e[2]; dist[e[1]][e[0]] = e[2]; }

    // Floyd-Warshall
    for (int k = 0; k < n; k++)
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                dist[i][j] = Math.min(dist[i][j], dist[i][k] + dist[k][j]);

    int result = 0, minReachable = n;
    for (int i = 0; i < n; i++) {
        int count = 0;
        for (int j = 0; j < n; j++) if (i != j && dist[i][j] <= distanceThreshold) count++;
        if (count <= minReachable) { minReachable = count; result = i; }
    }
    return result;
}
```

## Complexity — O(n³) time, O(n²) space
