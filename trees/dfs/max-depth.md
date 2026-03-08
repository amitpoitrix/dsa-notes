# Maximum Depth of Binary Tree — LC #104

**Pattern:** DFS (Postorder)
**Difficulty:** Easy
**Companies:** Amazon · Google · Meta

---

## Problem

Return the maximum depth of a binary tree.

```
Input:  [3,9,20,null,null,15,7]
Output: 3
```

---

## Code — Java

```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

---

## Complexity — O(n) time, O(h) space (h = height)
