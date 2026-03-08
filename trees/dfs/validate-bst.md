# Validate Binary Search Tree — LC #98

**Pattern:** DFS with Bounds
**Difficulty:** Medium
**Companies:** Amazon · Microsoft · Google

---

## Problem

Determine if a binary tree is a valid BST.

---

## Intuition

Each node must lie within a valid range (min, max). Pass bounds down recursively. Left child: max = parent val. Right child: min = parent val.

---

## Code — Java

```java
public boolean isValidBST(TreeNode root) {
    return validate(root, Long.MIN_VALUE, Long.MAX_VALUE);
}

private boolean validate(TreeNode node, long min, long max) {
    if (node == null) return true;
    if (node.val <= min || node.val >= max) return false;
    return validate(node.left, min, node.val) && validate(node.right, node.val, max);
}
```

---

## Complexity — O(n) time, O(h) space

---

## Common Mistakes

- Only checking left < root < right without propagating bounds — fails for cases like [5,4,6,null,null,3,7] where 3 is in right subtree of 5 but left subtree of 6.
