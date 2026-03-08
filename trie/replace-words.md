# Replace Words — LC #648

**Pattern:** Trie
**Difficulty:** Medium
**Companies:** Amazon · Uber

---

## Problem

Given a dictionary of root words and a sentence, replace every word in the sentence with its shortest root from the dictionary. If multiple roots match, use the shortest.

```
Input:  dictionary = ["cat","bat","rat"], sentence = "the cattle was rattled by the battery"
Output: "the cat was rat by the bat"
```

---

## Intuition

Insert all roots into a Trie. For each word in the sentence, traverse the Trie character by character. Return as soon as we hit an `isEnd` node — that's the shortest matching root.

---

## Code — Java

```java
public String replaceWords(List<String> dictionary, String sentence) {
    TrieNode root = new TrieNode();
    for (String root_ : dictionary) {
        TrieNode curr = root;
        for (char c : root_.toCharArray()) {
            int i = c - 'a';
            if (curr.children[i] == null) curr.children[i] = new TrieNode();
            curr = curr.children[i];
        }
        curr.isEnd = true;
    }

    StringBuilder sb = new StringBuilder();
    for (String word : sentence.split(" ")) {
        if (sb.length() > 0) sb.append(' ');
        sb.append(findRoot(root, word));
    }
    return sb.toString();
}

private String findRoot(TrieNode root, String word) {
    TrieNode curr = root;
    for (int i = 0; i < word.length(); i++) {
        int idx = word.charAt(i) - 'a';
        if (curr.children[idx] == null) break;
        curr = curr.children[idx];
        if (curr.isEnd) return word.substring(0, i + 1); // shortest root
    }
    return word; // no root found
}

class TrieNode {
    TrieNode[] children = new TrieNode[26];
    boolean isEnd;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(D + S) | D = total dict chars, S = sentence chars |
| Space | O(D * 26) | Trie nodes |

---

## Related Problems

- **Implement Trie (LC 208)** — base
- **Longest Word in Dictionary (LC 720)** — find longest word built char by char
