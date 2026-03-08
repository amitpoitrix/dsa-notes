# Invert Binary Tree — LC #226

**Pattern:** DFS
**Difficulty:** Easy

---

## Code — Java

```java
public TreeNode invertTree(TreeNode root) {
    if (root == null) return null;
    TreeNode temp = root.left;
    root.left = invertTree(root.right);
    root.right = invertTree(temp);
    return root;
}
```

## Complexity — O(n) time, O(h) space
