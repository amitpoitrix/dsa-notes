# Network Delay Time — LC #743

**Pattern:** Dijkstra
**Difficulty:** Medium
**Companies:** Google · Amazon · Uber

---

## Problem

`n` nodes, `times[i] = [u, v, w]` (edge u→v with weight w). Return min time for signal from `k` to reach all nodes, or -1 if impossible.

---

## Code — Java (Dijkstra)

```java
public int networkDelayTime(int[][] times, int n, int k) {
    Map<Integer, List<int[]>> adj = new HashMap<>();
    for (int[] t : times) adj.computeIfAbsent(t[0], x -> new ArrayList<>()).add(new int[]{t[1], t[2]});

    int[] dist = new int[n+1];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[k] = 0;

    PriorityQueue<int[]> pq = new PriorityQueue<>((a,b) -> a[1]-b[1]);
    pq.offer(new int[]{k, 0});

    while (!pq.isEmpty()) {
        int[] curr = pq.poll();
        int node = curr[0], d = curr[1];
        if (d > dist[node]) continue; // stale
        for (int[] next : adj.getOrDefault(node, new ArrayList<>())) {
            int newDist = dist[node] + next[1];
            if (newDist < dist[next[0]]) {
                dist[next[0]] = newDist;
                pq.offer(new int[]{next[0], newDist});
            }
        }
    }

    int max = 0;
    for (int i = 1; i <= n; i++) {
        if (dist[i] == Integer.MAX_VALUE) return -1;
        max = Math.max(max, dist[i]);
    }
    return max;
}
```

---

## Complexity — O((V+E) log V) time
