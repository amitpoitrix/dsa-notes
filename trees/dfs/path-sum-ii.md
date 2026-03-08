# Path Sum II — LC #113

**Pattern:** DFS + Backtracking
**Difficulty:** Medium
**Companies:** Amazon · Microsoft

---

## Problem

Find all root-to-leaf paths where sum equals `targetSum`.

---

## Code — Java

```java
public List<List<Integer>> pathSum(TreeNode root, int target) {
    List<List<Integer>> result = new ArrayList<>();
    dfs(root, target, new ArrayList<>(), result);
    return result;
}

private void dfs(TreeNode node, int remaining, List<Integer> path, List<List<Integer>> result) {
    if (node == null) return;
    path.add(node.val);

    if (node.left == null && node.right == null && remaining == node.val) {
        result.add(new ArrayList<>(path)); // copy path
    }
    dfs(node.left, remaining - node.val, path, result);
    dfs(node.right, remaining - node.val, path, result);

    path.remove(path.size() - 1); // backtrack
}
```

---

## Common Mistakes

- Adding `path` directly instead of `new ArrayList<>(path)` — all entries reference same list.
- Not backtracking — removes last element after both children explored.
