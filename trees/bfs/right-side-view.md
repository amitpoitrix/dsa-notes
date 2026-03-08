# Binary Tree Right Side View — LC #199

**Pattern:** BFS (Last Element per Level)
**Difficulty:** Medium
**Companies:** Amazon · Meta · Google

---

## Problem

Return the values of nodes visible from the right side.

---

## Code — Java

```java
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            if (i == size - 1) result.add(node.val); // last node of level
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
    }
    return result;
}
```

## Complexity — O(n) time and space
