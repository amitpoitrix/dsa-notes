# Diameter of Binary Tree — LC #543

**Pattern:** DFS (Return Height, Track Global Max)
**Difficulty:** Easy
**Companies:** Amazon · Google · Meta

---

## Problem

Return the length of the longest path between any two nodes (may or may not pass through root).

```
Input:  [1,2,3,4,5]
Output: 3   // path: 4→2→1→3 or 5→2→1→3
```

---

## Intuition

For each node, diameter through it = left height + right height. Track max globally. Return height to parent.

---

## Code — Java

```java
int maxDiam = 0;

public int diameterOfBinaryTree(TreeNode root) {
    height(root);
    return maxDiam;
}

private int height(TreeNode node) {
    if (node == null) return 0;
    int left = height(node.left);
    int right = height(node.right);
    maxDiam = Math.max(maxDiam, left + right);
    return 1 + Math.max(left, right);
}
```

---

## Complexity — O(n) time, O(h) space

---

## Common Mistakes

- Returning diameter instead of height from helper — parent needs height, not diameter.
