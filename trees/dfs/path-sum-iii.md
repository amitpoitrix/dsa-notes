# Path Sum III — LC #437

**Pattern:** DFS + Prefix Sum + HashMap
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta

---

## Problem

Count paths in a binary tree (not necessarily root-to-leaf) that sum to `targetSum`.

---

## Intuition

Same as "Subarray Sum Equals K" but on a tree. Use prefix sum + HashMap. The path from any ancestor to current node has sum = `currentSum - ancestorSum`. If `currentSum - target` exists in the map, found a valid path.

---

## Code — Java

```java
public int pathSum(TreeNode root, int targetSum) {
    Map<Long, Integer> map = new HashMap<>();
    map.put(0L, 1);
    return dfs(root, 0, targetSum, map);
}

private int dfs(TreeNode node, long curr, int target, Map<Long, Integer> map) {
    if (node == null) return 0;
    curr += node.val;
    int count = map.getOrDefault(curr - target, 0);
    map.put(curr, map.getOrDefault(curr, 0) + 1);
    count += dfs(node.left, curr, target, map) + dfs(node.right, curr, target, map);
    map.put(curr, map.get(curr) - 1); // backtrack
    return count;
}
```

---

## Complexity — O(n) time, O(n) space

---

## Common Mistakes

- Not backtracking the prefix map — removes count when returning up the tree.
- Using `int` for sum — can overflow with large trees.
