# Construct BT from Preorder + Inorder — LC #105

**Pattern:** Recursive Build
**Difficulty:** Medium
**Companies:** Amazon · Google · Microsoft

---

## Problem

Given preorder and inorder traversals, construct the binary tree.

---

## Intuition

Preorder[0] is always root. Find it in inorder — elements left of it are left subtree, elements right are right subtree. Recurse with appropriate subarrays.

---

## Code — Java

```java
public TreeNode buildTree(int[] preorder, int[] inorder) {
    Map<Integer, Integer> inMap = new HashMap<>();
    for (int i = 0; i < inorder.length; i++) inMap.put(inorder[i], i);
    return build(preorder, 0, 0, inorder.length - 1, inMap);
}

private TreeNode build(int[] pre, int preIdx, int inLeft, int inRight, Map<Integer, Integer> inMap) {
    if (inLeft > inRight) return null;
    int rootVal = pre[preIdx];
    TreeNode root = new TreeNode(rootVal);
    int mid = inMap.get(rootVal);
    int leftSize = mid - inLeft;
    root.left = build(pre, preIdx + 1, inLeft, mid - 1, inMap);
    root.right = build(pre, preIdx + leftSize + 1, mid + 1, inRight, inMap);
    return root;
}
```

---

## Complexity — O(n) time with HashMap, O(n) space
