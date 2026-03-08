# Sequence Reconstruction — LC #444

**Pattern:** Topological Sort (Unique Order Check)
**Difficulty:** Medium

---

## Problem

Check if `org` is the only shortest supersequence reconstructable from `seqs`.

---

## Intuition

Build graph from seqs. Run topological sort — if at any point queue has > 1 node, the order is not unique. The result must equal `org`.

---

## Code — Java

```java
public boolean sequenceReconstruction(int[] org, List<List<Integer>> seqs) {
    Map<Integer, Set<Integer>> adj = new HashMap<>();
    Map<Integer, Integer> inDegree = new HashMap<>();
    for (List<Integer> seq : seqs) for (int n : seq) { adj.putIfAbsent(n, new HashSet<>()); inDegree.putIfAbsent(n, 0); }
    for (List<Integer> seq : seqs)
        for (int i = 0; i < seq.size()-1; i++)
            if (adj.get(seq.get(i)).add(seq.get(i+1))) inDegree.merge(seq.get(i+1), 1, Integer::sum);

    Queue<Integer> queue = new LinkedList<>();
    for (int n : inDegree.keySet()) if (inDegree.get(n) == 0) queue.offer(n);

    int idx = 0;
    while (queue.size() == 1) {
        int n = queue.poll();
        if (idx >= org.length || org[idx++] != n) return false;
        for (int next : adj.get(n)) if (inDegree.merge(next, -1, Integer::sum) == 0) queue.offer(next);
    }
    return idx == org.length && queue.isEmpty();
}
```

## Complexity — O(V + E) time and space
