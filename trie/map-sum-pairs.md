# Map Sum Pairs — LC #677

**Pattern:** Trie with Values
**Difficulty:** Medium
**Companies:** Google

---

## Problem

Implement `MapSum` with `insert(key, val)` and `sum(prefix)` which returns the sum of all values whose keys start with `prefix`.

```
MapSum ms = new MapSum();
ms.insert("apple", 3);
ms.sum("ap");    // 3
ms.insert("app", 2);
ms.sum("ap");    // 5
```

---

## Intuition

Store value at the end node of each key in the Trie. `sum(prefix)` traverses to the prefix node, then DFS/sums all `val` in the subtree.

**Optimization:** Store cumulative sum at each node. When inserting, add the value (minus old value if key already exists) to every node along the path.

---

## Code — Java

```java
class MapSum {
    private Map<String, Integer> map = new HashMap<>();
    private TrieNode root = new TrieNode();

    public void insert(String key, int val) {
        int delta = val - map.getOrDefault(key, 0);
        map.put(key, val);
        TrieNode curr = root;
        curr.sum += delta;
        for (char c : key.toCharArray()) {
            int i = c - 'a';
            if (curr.children[i] == null) curr.children[i] = new TrieNode();
            curr = curr.children[i];
            curr.sum += delta;
        }
    }

    public int sum(String prefix) {
        TrieNode curr = root;
        for (char c : prefix.toCharArray()) {
            int i = c - 'a';
            if (curr.children[i] == null) return 0;
            curr = curr.children[i];
        }
        return curr.sum;
    }
}

class TrieNode {
    TrieNode[] children = new TrieNode[26];
    int sum;
}
```

---

## Complexity

| Operation | Time |
|-----------|------|
| insert    | O(L) |
| sum       | O(L) |

---

## Common Mistakes

- Not handling key updates — if same key inserted twice with new value, must compute delta to avoid double counting.

---

## Related Problems

- **Implement Trie (LC 208)** — base Trie
- **Replace Words (LC 648)** — prefix operations
