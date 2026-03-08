# Course Schedule I — LC #207

**Pattern:** Topological Sort / Cycle Detection
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Given `numCourses` and prerequisites `[a, b]` (take b before a), determine if you can finish all courses.

---

## Intuition

Build directed graph. Check for cycle — if cycle exists, impossible. Use Kahn's algorithm (BFS) or DFS.

---

## Code — Java (Kahn's BFS)

```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
    int[] inDegree = new int[numCourses];
    List<List<Integer>> adj = new ArrayList<>();
    for (int i = 0; i < numCourses; i++) adj.add(new ArrayList<>());

    for (int[] pre : prerequisites) {
        adj.get(pre[1]).add(pre[0]);
        inDegree[pre[0]]++;
    }

    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < numCourses; i++) if (inDegree[i] == 0) queue.offer(i);

    int processed = 0;
    while (!queue.isEmpty()) {
        int course = queue.poll();
        processed++;
        for (int next : adj.get(course)) {
            if (--inDegree[next] == 0) queue.offer(next);
        }
    }
    return processed == numCourses;
}
```

---

## Complexity — O(V + E) time and space
