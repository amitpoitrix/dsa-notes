# Convert Sorted Array to BST — LC #108

**Pattern:** Recursive Build (Mid as Root)
**Difficulty:** Easy
**Companies:** Amazon · Microsoft

---

## Problem

Convert sorted array to height-balanced BST.

---

## Code — Java

```java
public TreeNode sortedArrayToBST(int[] nums) {
    return build(nums, 0, nums.length - 1);
}

private TreeNode build(int[] nums, int left, int right) {
    if (left > right) return null;
    int mid = left + (right - left) / 2;
    TreeNode root = new TreeNode(nums[mid]);
    root.left = build(nums, left, mid - 1);
    root.right = build(nums, mid + 1, right);
    return root;
}
```

## Complexity — O(n) time, O(log n) space
