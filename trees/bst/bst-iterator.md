# BST Iterator — LC #173

**Pattern:** Controlled Inorder Traversal
**Difficulty:** Medium
**Companies:** Microsoft · LinkedIn · Google

---

## Problem

Implement iterator over BST with `next()` and `hasNext()`. O(h) memory, average O(1) `next()`.

---

## Code — Java

```java
class BSTIterator {
    private Deque<TreeNode> stack = new ArrayDeque<>();

    public BSTIterator(TreeNode root) {
        pushLeft(root);
    }

    public int next() {
        TreeNode node = stack.pop();
        pushLeft(node.right);
        return node.val;
    }

    public boolean hasNext() {
        return !stack.isEmpty();
    }

    private void pushLeft(TreeNode node) {
        while (node != null) { stack.push(node); node = node.left; }
    }
}
```

## Complexity — O(h) space, amortized O(1) per next()
