# Sort Colors — LC #75

**Pattern:** Two Pointers (Dutch National Flag — 3-way partition)
**Difficulty:** Medium
**Companies:** Microsoft · Amazon · Adobe · Uber

---

## Problem

Given array `nums` with values 0, 1, 2 (representing red, white, blue), sort them in-place so all 0s come first, then 1s, then 2s. Must be done in one pass without using a sort function.

```
Input:  [2, 0, 2, 1, 1, 0]
Output: [0, 0, 1, 1, 2, 2]

Input:  [2, 0, 1]
Output: [0, 1, 2]
```

---

## Intuition

**Dutch National Flag algorithm** by Dijkstra. Use three pointers:
- `low` — boundary of 0s region (everything left of `low` is 0).
- `mid` — current element being examined.
- `high` — boundary of 2s region (everything right of `high` is 2).

Process `mid` until it meets `high`:
- `nums[mid] == 0` → swap with `low`, advance both `low` and `mid`.
- `nums[mid] == 1` → it's in the right place, advance `mid`.
- `nums[mid] == 2` → swap with `high`, move `high` left. Don't advance `mid` (swapped element not yet examined).

---

## Algorithm

1. Set `low = 0`, `mid = 0`, `high = n - 1`.
2. While `mid <= high`:
   - `nums[mid] == 0` → swap(low, mid), `low++`, `mid++`.
   - `nums[mid] == 1` → `mid++`.
   - `nums[mid] == 2` → swap(mid, high), `high--`. (do NOT mid++)

---

## Code — Java

```java
public void sortColors(int[] nums) {
    int low = 0, mid = 0, high = nums.length - 1;

    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums, low, mid);
            low++;
            mid++;
        } else if (nums[mid] == 1) {
            mid++;
        } else {
            swap(nums, mid, high);
            high--;
            // don't increment mid — need to re-examine swapped element
        }
    }
}

private void swap(int[] nums, int i, int j) {
    int temp = nums[i];
    nums[i] = nums[j];
    nums[j] = temp;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Single pass, `mid` and `high` each move at most n times |
| Space | O(1) | In-place |

---

## Dry Run — [2, 0, 2, 1, 1, 0]

| low | mid | high | nums[mid] | Action | Array |
|-----|-----|------|-----------|--------|-------|
| 0   | 0   | 5    | 2         | swap(0,5), high-- | [0,0,2,1,1,2] |
| 0   | 0   | 4    | 0         | swap(0,0), low++, mid++ | [0,0,2,1,1,2] |
| 1   | 1   | 4    | 0         | swap(1,1), low++, mid++ | [0,0,2,1,1,2] |
| 2   | 2   | 4    | 2         | swap(2,4), high-- | [0,0,1,1,2,2] |
| 2   | 2   | 3    | 1         | mid++ | [0,0,1,1,2,2] |
| 2   | 3   | 3    | 1         | mid++ | [0,0,1,1,2,2] |
| 2   | 4   | 3    | —         | mid > high, stop | |

**Result:** [0, 0, 1, 1, 2, 2]

---

## Edge Cases

- **All same** `[1, 1, 1]` → unchanged.
- **Already sorted** `[0, 1, 2]` → unchanged.
- **Reverse sorted** `[2, 1, 0]` → correctly sorted in one pass.
- **Single element** `[0]` → unchanged.

---

## Common Mistakes

- Incrementing `mid` after swapping with `high` — the element swapped from `high` hasn't been examined yet, so `mid` must stay.
- Using two passes (count + fill) — correct but misses the point. One-pass with three pointers is what the problem wants.

---

## Related Problems

- **Move Zeroes (LC 283)** — simpler 2-region version of this
- **Remove Duplicates (LC 26)** — same slow/fast pointer family
- **Wiggle Sort (LC 280)** — similar in-place partition idea
