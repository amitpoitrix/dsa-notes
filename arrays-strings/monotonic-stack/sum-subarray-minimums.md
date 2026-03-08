# Sum of Subarray Minimums — LC #907

**Pattern:** Monotonic Stack + Contribution Technique
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem

Given array `arr`, find the sum of `min(subarray)` for all subarrays. Return result mod 10^9+7.

```
Input:  [3, 1, 2, 4]
Output: 17   // min of [3]=3,[1]=1,[2]=2,[4]=4,[3,1]=1,[1,2]=1,[2,4]=2,[3,1,2]=1,[1,2,4]=1,[3,1,2,4]=1 → sum=17
```

---

## Intuition

For each element `arr[i]`, find how many subarrays have `arr[i]` as their minimum. If `left[i]` = distance to previous smaller element and `right[i]` = distance to next smaller element, then `arr[i]` contributes `arr[i] * left[i] * right[i]` to the total.

Use monotonic stack to compute left and right boundaries efficiently.

---

## Code — Java

```java
public int sumSubarrayMins(int[] arr) {
    int MOD = 1_000_000_007;
    int n = arr.length;
    int[] left = new int[n];  // distance to previous smaller
    int[] right = new int[n]; // distance to next smaller or equal

    Deque<Integer> stack = new ArrayDeque<>();

    // previous smaller
    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && arr[stack.peek()] >= arr[i]) stack.pop();
        left[i] = stack.isEmpty() ? i + 1 : i - stack.peek();
        stack.push(i);
    }

    stack.clear();

    // next smaller or equal
    for (int i = n - 1; i >= 0; i--) {
        while (!stack.isEmpty() && arr[stack.peek()] > arr[i]) stack.pop();
        right[i] = stack.isEmpty() ? n - i : stack.peek() - i;
        stack.push(i);
    }

    long result = 0;
    for (int i = 0; i < n; i++) {
        result = (result + (long) arr[i] * left[i] * right[i]) % MOD;
    }
    return (int) result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Two passes |
| Space | O(n) | Stack + arrays |

---

## Key Detail

Use strict `>=` for left and `>` for right to avoid double counting duplicates.

---

## Related Problems

- **Largest Rectangle in Histogram (LC 84)** — same boundary concept
