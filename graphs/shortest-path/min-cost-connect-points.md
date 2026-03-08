# Minimum Cost to Connect All Points — LC #1584

**Pattern:** Prim's Algorithm (MST)
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Connect all points with minimum total Manhattan distance (MST).

---

## Code — Java (Prim's)

```java
public int minCostConnectPoints(int[][] points) {
    int n = points.length;
    boolean[] visited = new boolean[n];
    int[] minDist = new int[n];
    Arrays.fill(minDist, Integer.MAX_VALUE);
    minDist[0] = 0;

    PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[1]-b[1]);
    pq.offer(new int[]{0, 0});
    int total = 0;

    while (!pq.isEmpty()) {
        int[] curr = pq.poll();
        int node = curr[0], cost = curr[1];
        if (visited[node]) continue;
        visited[node] = true;
        total += cost;
        for (int j = 0; j < n; j++) {
            if (!visited[j]) {
                int d = Math.abs(points[node][0]-points[j][0]) + Math.abs(points[node][1]-points[j][1]);
                if (d < minDist[j]) { minDist[j] = d; pq.offer(new int[]{j, d}); }
            }
        }
    }
    return total;
}
```

## Complexity — O(n² log n) time
