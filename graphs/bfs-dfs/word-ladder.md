# Word Ladder — LC #127

**Pattern:** BFS (Shortest Path)
**Difficulty:** Hard
**Companies:** Google · Amazon · Meta

---

## Problem

Given `beginWord`, `endWord`, and `wordList`, find the length of the shortest transformation sequence. Each step changes exactly one letter and must be in wordList.

```
Input:  beginWord="hit", endWord="cog", wordList=["hot","dot","dog","lot","log","cog"]
Output: 5   // hit→hot→dot→dog→cog
```

---

## Intuition

BFS — each word is a node, connected if they differ by one letter. Find shortest path from beginWord to endWord.

---

## Code — Java

```java
public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    Set<String> wordSet = new HashSet<>(wordList);
    if (!wordSet.contains(endWord)) return 0;

    Queue<String> queue = new LinkedList<>();
    queue.offer(beginWord);
    int steps = 1;

    while (!queue.isEmpty()) {
        int size = queue.size();
        for (int i = 0; i < size; i++) {
            String word = queue.poll();
            char[] chars = word.toCharArray();
            for (int j = 0; j < chars.length; j++) {
                char orig = chars[j];
                for (char c = 'a'; c <= 'z'; c++) {
                    chars[j] = c;
                    String newWord = new String(chars);
                    if (newWord.equals(endWord)) return steps + 1;
                    if (wordSet.contains(newWord)) {
                        queue.offer(newWord);
                        wordSet.remove(newWord); // mark visited
                    }
                }
                chars[j] = orig;
            }
        }
        steps++;
    }
    return 0;
}
```

---

## Complexity — O(m² * n) where m = word length, n = wordList size
