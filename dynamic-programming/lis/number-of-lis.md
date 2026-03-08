# Number of Longest Increasing Subsequences — LC #673

**Pattern:** DP (LIS + Count)
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Given array, return the number of longest increasing subsequences.

```
Input:  nums = [1,3,5,4,7]
Output: 2   // [1,3,5,7] and [1,3,4,7]
```

---

## Intuition

Two DP arrays: `len[i]` = length of LIS ending at `i`, `cnt[i]` = count of such LIS. For each `j < i`: if `nums[j] < nums[i]`:
- If `len[j]+1 > len[i]`: update `len[i]`, `cnt[i] = cnt[j]`.
- If `len[j]+1 == len[i]`: `cnt[i] += cnt[j]`.

Answer = sum of `cnt[i]` for all `i` where `len[i] == maxLen`.

---

## Code — Java

```java
public int findNumberOfLIS(int[] nums) {
    int n = nums.length;
    int[] len = new int[n], cnt = new int[n];
    Arrays.fill(len, 1); Arrays.fill(cnt, 1);
    int maxLen = 1;

    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (nums[j] < nums[i]) {
                if (len[j] + 1 > len[i]) { len[i] = len[j]+1; cnt[i] = cnt[j]; }
                else if (len[j] + 1 == len[i]) { cnt[i] += cnt[j]; }
            }
        }
        maxLen = Math.max(maxLen, len[i]);
    }

    int result = 0;
    for (int i = 0; i < n; i++) if (len[i] == maxLen) result += cnt[i];
    return result;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n²) |
| Space | O(n) |

---

## Related Problems

- **LIS (LC 300)** — just the length
