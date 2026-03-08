# N-Queens — LC #51

**Pattern:** Backtracking + Constraint Checking
**Difficulty:** Hard
**Companies:** Amazon · Google · Microsoft

---

## Problem

Place `n` queens on an `n x n` chessboard so no two queens attack each other. Return all distinct solutions.

```
Input:  n = 4
Output: [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
```

---

## Intuition

Place one queen per row. For each column in the current row, check if it's safe (no conflict with any previously placed queen in same column, or either diagonal). Use sets to track occupied columns and diagonals for O(1) lookup.

---

## Code — Java

```java
public List<List<String>> solveNQueens(int n) {
    List<List<String>> result = new ArrayList<>();
    backtrack(n, 0, new int[n], new HashSet<>(), new HashSet<>(), new HashSet<>(), result);
    return result;
}

private void backtrack(int n, int row, int[] queens,
        Set<Integer> cols, Set<Integer> diag1, Set<Integer> diag2,
        List<List<String>> result) {
    if (row == n) {
        result.add(buildBoard(queens, n));
        return;
    }
    for (int col = 0; col < n; col++) {
        if (cols.contains(col) || diag1.contains(row - col) || diag2.contains(row + col))
            continue;
        queens[row] = col;
        cols.add(col); diag1.add(row - col); diag2.add(row + col);
        backtrack(n, row + 1, queens, cols, diag1, diag2, result);
        cols.remove(col); diag1.remove(row - col); diag2.remove(row + col);
    }
}

private List<String> buildBoard(int[] queens, int n) {
    List<String> board = new ArrayList<>();
    for (int row = 0; row < n; row++) {
        char[] line = new char[n];
        Arrays.fill(line, '.');
        line[queens[row]] = 'Q';
        board.add(new String(line));
    }
    return board;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n!) | n choices for row 1, n-1 for row 2... |
| Space | O(n) | Sets + recursion depth |

---

## Key Insight

Two queens are on same diagonal if:
- `row1 - col1 == row2 - col2` (top-left to bottom-right diagonal)
- `row1 + col1 == row2 + col2` (top-right to bottom-left diagonal)

---

## Common Mistakes

- Using a 2D board for conflict checking instead of 3 sets — O(n) check per placement vs O(1).

---

## Related Problems

- **Sudoku Solver (LC 37)** — 2D constraint backtracking
- **Permutations (LC 46)** — one-per-row constraint is like permutations
