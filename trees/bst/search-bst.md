# Search in BST — LC #700

**Pattern:** BST Property
**Difficulty:** Easy

---

## Code — Java

```java
public TreeNode searchBST(TreeNode root, int val) {
    if (root == null || root.val == val) return root;
    return val < root.val ? searchBST(root.left, val) : searchBST(root.right, val);
}
```

## Complexity — O(h) time
