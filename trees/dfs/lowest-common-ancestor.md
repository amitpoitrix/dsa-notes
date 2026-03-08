# Lowest Common Ancestor — LC #236

**Pattern:** DFS
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Find the lowest common ancestor (LCA) of two nodes p and q in a binary tree.

---

## Intuition

If current node is null, p, or q → return it. Recurse left and right. If both return non-null → current node is LCA. If only one returns non-null → propagate that up.

---

## Code — Java

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;

    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);

    if (left != null && right != null) return root; // p and q in different subtrees
    return left != null ? left : right;
}
```

---

## Complexity — O(n) time, O(h) space

---

## BST Variant (LC 235)

For BST: if both p, q < root → go left. If both > root → go right. Else root is LCA.
