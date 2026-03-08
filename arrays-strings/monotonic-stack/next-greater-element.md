# Next Greater Element I & II — LC #496 / #503

**Pattern:** Monotonic Decreasing Stack
**Difficulty:** Medium
**Companies:** Amazon · Google

---

## Problem I (LC 496)

`nums1` is a subset of `nums2`. For each element in `nums1`, find the next greater element in `nums2`. Return -1 if none.

```
Input:  nums1 = [4,1,2], nums2 = [1,3,4,2]
Output: [-1,3,-1]
```

---

## Problem II (LC 503)

Given circular array `nums`, find the next greater element for each element (can wrap around).

```
Input:  [1, 2, 1]
Output: [2,-1,2]
```

---

## Code — Java (LC 496)

```java
public int[] nextGreaterElement(int[] nums1, int[] nums2) {
    Map<Integer, Integer> map = new HashMap<>(); // value → next greater value
    Deque<Integer> stack = new ArrayDeque<>();

    for (int n : nums2) {
        while (!stack.isEmpty() && n > stack.peek()) {
            map.put(stack.pop(), n);
        }
        stack.push(n);
    }

    int[] result = new int[nums1.length];
    for (int i = 0; i < nums1.length; i++) {
        result[i] = map.getOrDefault(nums1[i], -1);
    }
    return result;
}
```

---

## Code — Java (LC 503 — Circular)

```java
public int[] nextGreaterElements(int[] nums) {
    int n = nums.length;
    int[] result = new int[n];
    Arrays.fill(result, -1);
    Deque<Integer> stack = new ArrayDeque<>(); // indices

    for (int i = 0; i < 2 * n; i++) {  // iterate twice for circular
        while (!stack.isEmpty() && nums[i % n] > nums[stack.peek()]) {
            result[stack.pop()] = nums[i % n];
        }
        if (i < n) stack.push(i);
    }
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each element pushed and popped once |
| Space | O(n) | Stack + map |

---

## Common Mistakes

- LC 503: forgetting to only push in the first pass (`if i < n`) — prevents duplicates on the stack.

---

## Related Problems

- **Daily Temperatures (LC 739)** — same pattern, return days not values
- **Largest Rectangle in Histogram (LC 84)** — monotonic stack
