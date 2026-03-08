# Average of Levels in Binary Tree — LC #637

**Pattern:** BFS
**Difficulty:** Easy

---

## Code — Java

```java
public List<Double> averageOfLevels(TreeNode root) {
    List<Double> result = new ArrayList<>();
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int size = queue.size();
        double sum = 0;
        for (int i = 0; i < size; i++) {
            TreeNode node = queue.poll();
            sum += node.val;
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        result.add(sum / size);
    }
    return result;
}
```

## Complexity — O(n) time and space
