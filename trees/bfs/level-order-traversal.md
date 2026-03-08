# Binary Tree Level Order Traversal — LC #102

**Pattern:** BFS Queue
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta

---

## Code — Java

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int size = queue.size();
        List<Integer> level = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            level.add(node.val);
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        result.add(level);
    }
    return result;
}
```

## Complexity — O(n) time and space

---

## Key Pattern

`int size = queue.size()` at the start of each while-loop iteration locks in the number of nodes at the current level.
