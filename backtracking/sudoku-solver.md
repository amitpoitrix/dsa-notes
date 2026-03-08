# Sudoku Solver — LC #37

**Pattern:** Backtracking + Constraint Propagation
**Difficulty:** Hard
**Companies:** Amazon · Google · Uber

---

## Problem

Solve a 9x9 Sudoku puzzle in-place. Empty cells marked with `'.'`. Each row, column, and 3x3 box must contain digits 1-9 without repetition.

---

## Intuition

Find first empty cell. Try digits 1-9. Check validity (not in same row, col, or 3x3 box). Place and recurse. If recursion fails, undo (backtrack) and try next digit.

---

## Code — Java

```java
public void solveSudoku(char[][] board) {
    solve(board);
}

private boolean solve(char[][] board) {
    for (int r = 0; r < 9; r++) {
        for (int c = 0; c < 9; c++) {
            if (board[r][c] == '.') {
                for (char d = '1'; d <= '9'; d++) {
                    if (isValid(board, r, c, d)) {
                        board[r][c] = d;
                        if (solve(board)) return true;
                        board[r][c] = '.'; // backtrack
                    }
                }
                return false; // no digit works, backtrack
            }
        }
    }
    return true; // all cells filled
}

private boolean isValid(char[][] board, int row, int col, char d) {
    for (int i = 0; i < 9; i++) {
        if (board[row][i] == d) return false; // same row
        if (board[i][col] == d) return false; // same col
        // same 3x3 box
        int r = 3 * (row / 3) + i / 3;
        int c = 3 * (col / 3) + i % 3;
        if (board[r][c] == d) return false;
    }
    return true;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(9^m) | m = empty cells, 9 choices each |
| Space | O(m) | Recursion depth |

---

## Edge Cases

- Valid puzzle always has exactly one solution per problem constraints.
- Pre-filled cells must not be overwritten.

---

## Common Mistakes

- Not returning `false` when no digit fits — must propagate failure upward.
- The 3x3 box index formula: `row = 3*(r/3) + i/3`, `col = 3*(c/3) + i%3`.

---

## Related Problems

- **N-Queens (LC 51)** — constraint backtracking on 2D board
- **Valid Sudoku (LC 36)** — just validate, don't solve
