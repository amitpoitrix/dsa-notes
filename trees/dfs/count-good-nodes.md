# Count Good Nodes in Binary Tree — LC #1448

**Pattern:** DFS with Max Tracking
**Difficulty:** Medium

---

## Problem

A node is "good" if no node on the path from root to it has a value greater than its value.

---

## Code — Java

```java
public int goodNodes(TreeNode root) {
    return dfs(root, Integer.MIN_VALUE);
}

private int dfs(TreeNode node, int maxSoFar) {
    if (node == null) return 0;
    int good = node.val >= maxSoFar ? 1 : 0;
    int newMax = Math.max(maxSoFar, node.val);
    return good + dfs(node.left, newMax) + dfs(node.right, newMax);
}
```

## Complexity — O(n) time, O(h) space
