# Serialize and Deserialize Binary Tree — LC #297

**Pattern:** DFS Encode/Decode
**Difficulty:** Hard
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Design serialization and deserialization of a binary tree.

---

## Code — Java (Preorder DFS)

```java
public String serialize(TreeNode root) {
    if (root == null) return "N,";
    return root.val + "," + serialize(root.left) + serialize(root.right);
}

public TreeNode deserialize(String data) {
    Queue<String> queue = new LinkedList<>(Arrays.asList(data.split(",")));
    return build(queue);
}

private TreeNode build(Queue<String> q) {
    String val = q.poll();
    if (val.equals("N")) return null;
    TreeNode node = new TreeNode(Integer.parseInt(val));
    node.left = build(q);
    node.right = build(q);
    return node;
}
```

---

## Complexity — O(n) time and space
