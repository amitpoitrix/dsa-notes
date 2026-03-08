# Design Add and Search Words — LC #211

**Pattern:** Trie + DFS (Wildcard)
**Difficulty:** Medium
**Companies:** Facebook · Google

---

## Problem

Design a data structure that supports `addWord` and `search`. Search may contain `.` which matches any letter.

```
WordDictionary wd = new WordDictionary();
wd.addWord("bad"); wd.addWord("dad");
wd.search("bad"); // true
wd.search(".ad"); // true
wd.search("b.."); // true
```

---

## Intuition

Standard Trie for `addWord`. For `search`, when we encounter `.`, recursively try all 26 children. When we encounter a letter, follow normally.

---

## Code — Java

```java
class WordDictionary {
    TrieNode root = new TrieNode();

    public void addWord(String word) {
        TrieNode curr = root;
        for (char c : word.toCharArray()) {
            int i = c - 'a';
            if (curr.children[i] == null) curr.children[i] = new TrieNode();
            curr = curr.children[i];
        }
        curr.isEnd = true;
    }

    public boolean search(String word) {
        return dfs(word, 0, root);
    }

    private boolean dfs(String word, int idx, TrieNode node) {
        if (idx == word.length()) return node.isEnd;
        char c = word.charAt(idx);
        if (c == '.') {
            for (TrieNode child : node.children)
                if (child != null && dfs(word, idx + 1, child)) return true;
            return false;
        }
        TrieNode next = node.children[c - 'a'];
        return next != null && dfs(word, idx + 1, next);
    }
}

class TrieNode {
    TrieNode[] children = new TrieNode[26];
    boolean isEnd;
}
```

---

## Complexity

| Operation | Time | Notes |
|-----------|------|-------|
| addWord   | O(L) | |
| search (no .)| O(L) | |
| search (all .)| O(26^L) | worst case |

---

## Common Mistakes

- Not handling `.` recursively — must try all 26 children, not just skip.

---

## Related Problems

- **Implement Trie (LC 208)** — base implementation
- **Word Search II (LC 212)** — Trie + backtracking on grid
