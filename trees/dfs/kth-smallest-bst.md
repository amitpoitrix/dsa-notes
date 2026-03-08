# Kth Smallest Element in BST — LC #230

**Pattern:** Inorder DFS
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta

---

## Problem

Find the kth smallest element in a BST.

---

## Intuition

Inorder traversal of BST gives sorted order. Stop at kth element.

---

## Code — Java (Iterative)

```java
public int kthSmallest(TreeNode root, int k) {
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode curr = root;

    while (curr != null || !stack.isEmpty()) {
        while (curr != null) { stack.push(curr); curr = curr.left; }
        curr = stack.pop();
        if (--k == 0) return curr.val;
        curr = curr.right;
    }
    return -1;
}
```

---

## Complexity — O(h + k) time, O(h) space
