# Binary Tree Vertical Order Traversal — LC #987

**Pattern:** BFS + Column Mapping
**Difficulty:** Hard
**Companies:** Meta · Amazon

---

## Problem

Return nodes column by column, sorted top-to-bottom within column. Ties sorted by value.

---

## Code — Java

```java
public List<List<Integer>> verticalTraversal(TreeNode root) {
    TreeMap<Integer, TreeMap<Integer, PriorityQueue<Integer>>> map = new TreeMap<>();
    Queue<int[]> queue = new LinkedList<>(); // [node_ref_trick: use wrapper]

    // Use DFS with coordinates instead
    dfs(root, 0, 0, map);

    List<List<Integer>> result = new ArrayList<>();
    for (TreeMap<Integer, PriorityQueue<Integer>> colMap : map.values()) {
        List<Integer> col = new ArrayList<>();
        for (PriorityQueue<Integer> pq : colMap.values()) {
            while (!pq.isEmpty()) col.add(pq.poll());
        }
        result.add(col);
    }
    return result;
}

private void dfs(TreeNode node, int col, int row, TreeMap<Integer, TreeMap<Integer, PriorityQueue<Integer>>> map) {
    if (node == null) return;
    map.computeIfAbsent(col, k -> new TreeMap<>())
       .computeIfAbsent(row, k -> new PriorityQueue<>())
       .offer(node.val);
    dfs(node.left, col - 1, row + 1, map);
    dfs(node.right, col + 1, row + 1, map);
}
```

## Complexity — O(n log n) time, O(n) space
