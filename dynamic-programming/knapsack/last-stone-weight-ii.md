# Last Stone Weight II — LC #1049

**Pattern:** 0/1 Knapsack
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Each stone has a positive weight. Smash two stones: if equal weights both destroyed, else larger minus smaller remains. Return minimum possible weight of last stone (or 0).

---

## Intuition

Assign each stone `+` or `-`. Minimize `|sum(+) - sum(-)|`. Same as partition: find subset closest to `total/2`. This minimizes the difference.

---

## Code — Java

```java
public int lastStoneWeightII(int[] stones) {
    int sum = 0;
    for (int s : stones) sum += s;
    int target = sum / 2;

    boolean[] dp = new boolean[target + 1];
    dp[0] = true;

    for (int stone : stones) {
        for (int j = target; j >= stone; j--) {
            dp[j] = dp[j] || dp[j - stone];
        }
    }

    for (int j = target; j >= 0; j--) {
        if (dp[j]) return sum - 2 * j;
    }
    return sum;
}
```

---

## Complexity

| | Complexity |
|---|---|
| Time  | O(n * sum) |
| Space | O(sum) |

---

## Related Problems

- **Partition Equal Subset Sum (LC 416)** — exact partition
- **Target Sum (LC 494)** — count ways
