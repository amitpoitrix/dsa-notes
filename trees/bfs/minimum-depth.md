# Minimum Depth of Binary Tree — LC #111

**Pattern:** BFS (First Leaf Found)
**Difficulty:** Easy
**Companies:** Amazon

---

## Problem

Find minimum depth (root to nearest leaf). BFS is better than DFS here — finds answer at first leaf.

---

## Code — Java

```java
public int minDepth(TreeNode root) {
    if (root == null) return 0;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    int depth = 1;

    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            if (node.left == null && node.right == null) return depth; // leaf!
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        depth++;
    }
    return depth;
}
```

## Complexity — O(n) worst, O(n) space. BFS can exit early unlike DFS.

---

## Common Mistakes

- Using DFS and forgetting that a node with only one child is NOT a leaf — minimum depth is NOT `1 + min(left, right)` when one side is null.
