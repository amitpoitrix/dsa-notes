# Minimum Height Trees — LC #310

**Pattern:** Leaf Trimming (Reverse Topo Sort)
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Find roots of minimum height trees in an undirected tree.

---

## Intuition

The roots are the "center" nodes of the tree. Trim leaves iteratively until 1 or 2 nodes remain.

---

## Code — Java

```java
public List<Integer> findMinHeightTrees(int n, int[][] edges) {
    if (n == 1) return Collections.singletonList(0);
    List<Set<Integer>> adj = new ArrayList<>();
    for (int i = 0; i < n; i++) adj.add(new HashSet<>());
    for (int[] e : edges) { adj.get(e[0]).add(e[1]); adj.get(e[1]).add(e[0]); }

    Queue<Integer> leaves = new LinkedList<>();
    for (int i = 0; i < n; i++) if (adj.get(i).size() == 1) leaves.offer(i);

    int remaining = n;
    while (remaining > 2) {
        int size = leaves.size(); remaining -= size;
        for (int i = 0; i < size; i++) {
            int leaf = leaves.poll();
            int neighbor = adj.get(leaf).iterator().next();
            adj.get(neighbor).remove(leaf);
            if (adj.get(neighbor).size() == 1) leaves.offer(neighbor);
        }
    }
    return new ArrayList<>(leaves);
}
```

---

## Complexity — O(n) time and space
