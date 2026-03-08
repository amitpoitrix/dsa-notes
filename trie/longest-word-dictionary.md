# Longest Word in Dictionary — LC #720

**Pattern:** Trie / HashSet
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Given array of strings `words`, return the longest word that can be built one character at a time by other words in the array. If tie, return lexicographically smallest.

```
Input:  words = ["a","banana","app","appl","ap","apply","apple"]
Output: "apple"
```

---

## Intuition

Insert all words into a Trie. BFS/DFS from root, only moving to a child if it marks the end of a word. The deepest reachable `isEnd` node with the longest path is the answer.

Alternatively: sort words, use a HashSet. For each word, check if `word[0..n-2]` is in the set. If yes, it can be built step by step.

---

## Code — Java (HashSet approach)

```java
public String longestWord(String[] words) {
    Arrays.sort(words); // sort so shorter words processed first
    Set<String> built = new HashSet<>();
    built.add("");
    String result = "";

    for (String word : words) {
        if (built.contains(word.substring(0, word.length() - 1))) {
            built.add(word);
            if (word.length() > result.length()) result = word;
        }
    }
    return result;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log n + n*L) | Sort + prefix check |
| Space | O(n*L) | HashSet stores all words |

---

## Common Mistakes

- Not sorting first — must ensure all prefixes are processed before longer words.

---

## Related Problems

- **Replace Words (LC 648)** — shortest prefix in Trie
- **Implement Trie (LC 208)** — Trie base
