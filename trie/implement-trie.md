# Implement Trie — LC #208

**Pattern:** Trie (Prefix Tree)
**Difficulty:** Medium
**Companies:** Google · Amazon · Facebook · Microsoft

---

## Problem

Implement a Trie with `insert`, `search`, and `startsWith` operations.

```
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");    // true
trie.search("app");      // false
trie.startsWith("app");  // true
```

---

## Intuition

A Trie is a tree where each node represents a character. Each path from root to a marked node spells out a word. Each node has up to 26 children (for lowercase letters) and a `isEnd` flag.

---

## Code — Java

```java
class Trie {
    private TrieNode root;

    public Trie() { root = new TrieNode(); }

    public void insert(String word) {
        TrieNode curr = root;
        for (char c : word.toCharArray()) {
            int idx = c - 'a';
            if (curr.children[idx] == null)
                curr.children[idx] = new TrieNode();
            curr = curr.children[idx];
        }
        curr.isEnd = true;
    }

    public boolean search(String word) {
        TrieNode node = getNode(word);
        return node != null && node.isEnd;
    }

    public boolean startsWith(String prefix) {
        return getNode(prefix) != null;
    }

    private TrieNode getNode(String s) {
        TrieNode curr = root;
        for (char c : s.toCharArray()) {
            int idx = c - 'a';
            if (curr.children[idx] == null) return null;
            curr = curr.children[idx];
        }
        return curr;
    }
}

class TrieNode {
    TrieNode[] children = new TrieNode[26];
    boolean isEnd = false;
}
```

---

## Complexity

| Operation | Time | Space |
|-----------|------|-------|
| insert    | O(L) | O(L) — new nodes |
| search    | O(L) | O(1) |
| startsWith| O(L) | O(1) |

L = word length. Total space O(26 * N * L) worst case.

---

## Edge Cases

- Search for prefix as word — must check `isEnd`, not just node existence.
- Insert same word twice — idempotent, just sets `isEnd = true` again.

---

## Common Mistakes

- Returning `true` in `search` just because node exists — must check `isEnd`.
- Using `HashMap<Character, TrieNode>` instead of array — works but slower constant factor.

---

## Related Problems

- **Design Add & Search Words (LC 211)** — wildcard search
- **Word Search II (LC 212)** — Trie + backtracking
- **Replace Words (LC 648)** — find shortest prefix in Trie
