# Parallel Courses — LC #1136

**Pattern:** Topological Sort + BFS Level Count
**Difficulty:** Medium

---

## Problem

Find minimum number of semesters to complete all courses given prerequisites.

---

## Intuition

Each BFS level = one semester. Count levels in topological sort.

---

## Code — Java

```java
public int minimumSemesters(int n, int[][] relations) {
    int[] inDegree = new int[n+1];
    List<List<Integer>> adj = new ArrayList<>();
    for (int i = 0; i <= n; i++) adj.add(new ArrayList<>());
    for (int[] r : relations) { adj.get(r[0]).add(r[1]); inDegree[r[1]]++; }

    Queue<Integer> queue = new LinkedList<>();
    for (int i = 1; i <= n; i++) if (inDegree[i] == 0) queue.offer(i);

    int semesters = 0, taken = 0;
    while (!queue.isEmpty()) {
        int size = queue.size(); semesters++;
        for (int i = 0; i < size; i++) {
            int c = queue.poll(); taken++;
            for (int next : adj.get(c)) if (--inDegree[next] == 0) queue.offer(next);
        }
    }
    return taken == n ? semesters : -1;
}
```

## Complexity — O(V + E) time and space
