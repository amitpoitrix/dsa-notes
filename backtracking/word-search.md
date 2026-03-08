# Word Search — LC #79

**Pattern:** Backtracking + DFS on Grid
**Difficulty:** Medium
**Companies:** Amazon · Microsoft · Facebook

---

## Problem

Given an `m x n` grid of characters and a string `word`, return `true` if word exists in the grid using adjacent (horizontally/vertically) cells. Each cell used at most once.

```
Input:  board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
Output: true
```

---

## Intuition

For each cell matching `word[0]`, start a DFS. Mark cells as visited by temporarily modifying them (or using a visited array). Explore all 4 directions. Backtrack by restoring the cell.

---

## Code — Java

```java
public boolean exist(char[][] board, String word) {
    for (int r = 0; r < board.length; r++)
        for (int c = 0; c < board[0].length; c++)
            if (dfs(board, word, r, c, 0)) return true;
    return false;
}

private boolean dfs(char[][] board, String word, int r, int c, int idx) {
    if (idx == word.length()) return true;
    if (r < 0 || r >= board.length || c < 0 || c >= board[0].length) return false;
    if (board[r][c] != word.charAt(idx)) return false;

    char temp = board[r][c];
    board[r][c] = '#'; // mark visited

    boolean found = dfs(board, word, r+1, c, idx+1) ||
                    dfs(board, word, r-1, c, idx+1) ||
                    dfs(board, word, r, c+1, idx+1) ||
                    dfs(board, word, r, c-1, idx+1);

    board[r][c] = temp; // restore
    return found;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(m*n * 4^L) | L = word length, 4 choices per step |
| Space | O(L) | Recursion depth = word length |

---

## Edge Cases

- Word longer than total cells → impossible.
- Single cell board matching single char word → true.

---

## Common Mistakes

- Forgetting to restore `board[r][c]` after DFS — permanently marks cells.
- Checking bounds after accessing board — check bounds first.

---

## Related Problems

- **Word Search II (LC 212)** — find multiple words using Trie
- **Number of Islands (LC 200)** — DFS on grid without backtracking
