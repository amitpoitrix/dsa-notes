# Insert and Delete in BST — LC #701 / #450

**Pattern:** BST Property
**Difficulty:** Medium

---

## Insert (LC 701)

```java
public TreeNode insertIntoBST(TreeNode root, int val) {
    if (root == null) return new TreeNode(val);
    if (val < root.val) root.left = insertIntoBST(root.left, val);
    else root.right = insertIntoBST(root.right, val);
    return root;
}
```

---

## Delete (LC 450)

Three cases: node has no children, one child, or two children.
For two children: replace with inorder successor (smallest in right subtree).

```java
public TreeNode deleteNode(TreeNode root, int key) {
    if (root == null) return null;
    if (key < root.val) root.left = deleteNode(root.left, key);
    else if (key > root.val) root.right = deleteNode(root.right, key);
    else {
        if (root.left == null) return root.right;
        if (root.right == null) return root.left;
        // two children: find inorder successor
        TreeNode successor = root.right;
        while (successor.left != null) successor = successor.left;
        root.val = successor.val;
        root.right = deleteNode(root.right, successor.val);
    }
    return root;
}
```

## Complexity — O(h) time, O(h) space
