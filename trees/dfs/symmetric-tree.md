# Symmetric Tree — LC #101

**Pattern:** DFS Mirror Check
**Difficulty:** Easy
**Companies:** Amazon · Microsoft

---

## Problem

Check if a binary tree is a mirror of itself.

---

## Code — Java

```java
public boolean isSymmetric(TreeNode root) {
    return isMirror(root.left, root.right);
}

private boolean isMirror(TreeNode l, TreeNode r) {
    if (l == null && r == null) return true;
    if (l == null || r == null) return false;
    return l.val == r.val && isMirror(l.left, r.right) && isMirror(l.right, r.left);
}
```

## Complexity — O(n) time, O(h) space
