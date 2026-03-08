# Binary Tree Maximum Path Sum — LC #124

**Pattern:** DFS (Return Max Gain, Track Global Max)
**Difficulty:** Hard
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Find the maximum path sum in a binary tree. A path goes through any sequence of nodes (doesn't need to pass through root).

```
Input:  [-10,9,20,null,null,15,7]
Output: 42   // path: 15→20→7
```

---

## Intuition

For each node, max path through it = node.val + max(0, left gain) + max(0, right gain). But we can only pass ONE side up to parent (can't split). Return max single-side gain to parent.

---

## Code — Java

```java
int maxSum = Integer.MIN_VALUE;

public int maxPathSum(TreeNode root) {
    gain(root);
    return maxSum;
}

private int gain(TreeNode node) {
    if (node == null) return 0;
    int left = Math.max(0, gain(node.left));   // ignore negative paths
    int right = Math.max(0, gain(node.right));
    maxSum = Math.max(maxSum, node.val + left + right); // path through node
    return node.val + Math.max(left, right);    // return best single side
}
```

---

## Complexity — O(n) time, O(h) space

---

## Common Mistakes

- Not using `Math.max(0, ...)` for children — negative subtrees should be ignored.
- Returning `left + right + node.val` to parent — you can only pick one side to extend.
