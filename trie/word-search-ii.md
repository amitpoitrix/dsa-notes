# Word Search II — LC #212

**Pattern:** Trie + Backtracking on Grid
**Difficulty:** Hard
**Companies:** Google · Amazon · Microsoft

---

## Problem

Given an `m x n` board and a list of words, find all words in the board (adjacent cells, each used once).

```
Input:  board = [["o","a","a","n"],["e","t","a","e"],["i","h","k","r"],["i","f","l","v"]],
        words = ["oath","pea","eat","rain"]
Output: ["eat","oath"]
```

---

## Intuition

Build a Trie from all words. DFS from each cell. At each step, follow the Trie — if no Trie child exists for current char, prune. When `isEnd` found, add to result. Mark cells visited during DFS.

This avoids repeating search for each word individually.

---

## Code — Java

```java
public List<String> findWords(char[][] board, String[] words) {
    TrieNode root = buildTrie(words);
    List<String> result = new ArrayList<>();
    for (int r = 0; r < board.length; r++)
        for (int c = 0; c < board[0].length; c++)
            dfs(board, root, r, c, result);
    return result;
}

private void dfs(char[][] board, TrieNode node, int r, int c, List<String> result) {
    if (r < 0 || r >= board.length || c < 0 || c >= board[0].length) return;
    char ch = board[r][c];
    if (ch == '#' || node.children[ch - 'a'] == null) return;

    node = node.children[ch - 'a'];
    if (node.word != null) {
        result.add(node.word);
        node.word = null; // avoid duplicates
    }

    board[r][c] = '#';
    dfs(board, node, r+1, c, result);
    dfs(board, node, r-1, c, result);
    dfs(board, node, r, c+1, result);
    dfs(board, node, r, c-1, result);
    board[r][c] = ch;
}

private TrieNode buildTrie(String[] words) {
    TrieNode root = new TrieNode();
    for (String w : words) {
        TrieNode curr = root;
        for (char c : w.toCharArray()) {
            int i = c - 'a';
            if (curr.children[i] == null) curr.children[i] = new TrieNode();
            curr = curr.children[i];
        }
        curr.word = w; // store word at end node
    }
    return root;
}

class TrieNode {
    TrieNode[] children = new TrieNode[26];
    String word; // non-null means end of a word
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(m*n * 4^L) | L = max word length |
| Space | O(W*L) | Trie size, W words |

---

## Common Mistakes

- Running DFS separately for each word — O(W * m*n * 4^L). Trie merges shared prefixes.
- Not setting `node.word = null` after finding — same word found multiple times.

---

## Related Problems

- **Word Search (LC 79)** — single word, no Trie needed
- **Implement Trie (LC 208)** — base Trie implementation
