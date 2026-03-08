# Daily Temperatures — LC #739

**Pattern:** Monotonic Decreasing Stack
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta · Microsoft

---

## Problem

Given `temperatures` array, return array where `answer[i]` = number of days until a warmer temperature. If no warmer day, answer is 0.

```
Input:  [73,74,75,71,69,72,76,73]
Output: [1,1,4,2,1,1,0,0]
```

---

## Intuition

Use a monotonic decreasing stack of indices. When a warmer day arrives, pop all colder days and compute the wait.

---

## Algorithm

1. Maintain stack of indices with decreasing temperatures.
2. For each `i`, while `temps[i] > temps[stack.top()]`:
   - Pop index `j`. `answer[j] = i - j`.
3. Push `i`.

---

## Code — Java

```java
public int[] dailyTemperatures(int[] temperatures) {
    int n = temperatures.length;
    int[] answer = new int[n];
    Deque<Integer> stack = new ArrayDeque<>(); // stores indices

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
            int j = stack.pop();
            answer[j] = i - j;
        }
        stack.push(i);
    }
    return answer;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n) | Each index pushed and popped at most once |
| Space | O(n) | Stack |

---

## Dry Run — [73,74,75,71,69,72,76,73]

- i=0: push 0. stack=[0]
- i=1: 74>73, pop 0 → ans[0]=1. Push 1. stack=[1]
- i=2: 75>74, pop 1 → ans[1]=1. Push 2. stack=[2]
- i=3: 71<75, push 3. stack=[2,3]
- i=4: 69<71, push 4. stack=[2,3,4]
- i=5: 72>69 pop4→ans[4]=1, 72>71 pop3→ans[3]=2, 72<75 stop. Push 5. stack=[2,5]
- i=6: 76>72 pop5→ans[5]=1, 76>75 pop2→ans[2]=4. Push 6. stack=[6]
- i=7: 73<76, push 7. Remaining: ans[6]=0, ans[7]=0.

**Result:** [1,1,4,2,1,1,0,0]

---

## Common Mistakes

- Storing temperatures in stack instead of indices — you need index to compute the difference.

---

## Related Problems

- **Next Greater Element I (LC 496)** — same pattern
- **Sum of Subarray Minimums (LC 907)** — monotonic stack contribution
