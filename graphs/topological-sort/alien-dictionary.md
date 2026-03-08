# Alien Dictionary — LC #269

**Pattern:** Topological Sort on Characters
**Difficulty:** Hard
**Companies:** Google · Meta · Amazon

---

## Problem

Given sorted list of alien language words, determine the character order.

---

## Algorithm

1. Compare adjacent words, find first differing characters → edge: char[i] → char[j].
2. Topological sort on the character graph.
3. If cycle exists or word[i] is prefix of word[j] but appears after → return "".

---

## Code — Java

```java
public String alienOrder(String[] words) {
    Map<Character, Set<Character>> adj = new HashMap<>();
    Map<Character, Integer> inDegree = new HashMap<>();
    for (String word : words) for (char c : word.toCharArray()) { adj.putIfAbsent(c, new HashSet<>()); inDegree.putIfAbsent(c, 0); }

    for (int i = 0; i < words.length - 1; i++) {
        String w1 = words[i], w2 = words[i+1];
        int minLen = Math.min(w1.length(), w2.length());
        if (w1.length() > w2.length() && w1.startsWith(w2)) return "";
        for (int j = 0; j < minLen; j++) {
            if (w1.charAt(j) != w2.charAt(j)) {
                if (adj.get(w1.charAt(j)).add(w2.charAt(j))) inDegree.merge(w2.charAt(j), 1, Integer::sum);
                break;
            }
        }
    }

    Queue<Character> queue = new LinkedList<>();
    for (char c : inDegree.keySet()) if (inDegree.get(c) == 0) queue.offer(c);
    StringBuilder sb = new StringBuilder();
    while (!queue.isEmpty()) {
        char c = queue.poll(); sb.append(c);
        for (char next : adj.get(c)) if (inDegree.merge(next, -1, Integer::sum) == 0) queue.offer(next);
    }
    return sb.length() == inDegree.size() ? sb.toString() : "";
}
```

---

## Complexity — O(C) where C = total characters in all words
