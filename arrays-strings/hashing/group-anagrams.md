# Group Anagrams — LC #49

**Pattern:** HashMap + Sorted Key
**Difficulty:** Medium
**Companies:** Google · Amazon · Meta · Microsoft

---

## Problem

Given array of strings `strs`, group the anagrams together.

```
Input:  ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
```

---

## Intuition

Anagrams have the same characters in different order. If we sort each word, all anagrams produce the same key. Group words by their sorted key in a HashMap.

---

## Algorithm

1. Create `HashMap<String, List<String>>`.
2. For each word: sort it → use as key → add word to that key's list.
3. Return all values.

---

## Code — Java

```java
public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> map = new HashMap<>();

    for (String word : strs) {
        char[] chars = word.toCharArray();
        Arrays.sort(chars);
        String key = new String(chars);
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(word);
    }
    return new ArrayList<>(map.values());
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n * k log k) | n words, each sorted in O(k log k) |
| Space | O(n * k)       | All strings stored in map |

---

## Dry Run — ["eat","tea","tan","ate","nat","bat"]

| word | sorted key | map |
|------|-----------|-----|
| eat  | aet       | {aet:[eat]} |
| tea  | aet       | {aet:[eat,tea]} |
| tan  | ant       | {aet:[eat,tea], ant:[tan]} |
| ate  | aet       | {aet:[eat,tea,ate], ...} |
| nat  | ant       | {..., ant:[tan,nat]} |
| bat  | abt       | {..., abt:[bat]} |

**Result:** [["eat","tea","ate"],["tan","nat"],["bat"]]

---

## Edge Cases

- Empty strings → sorted key is `""`, all empty strings grouped together.
- Single character words → trivially grouped.

---

## Common Mistakes

- Using word as key directly → doesn't group anagrams.
- Forgetting `computeIfAbsent` — need to initialize list if key not present.

---

## Optimization

Use frequency array as key instead of sorting → O(n * k) time.
Key = `"1#0#1#..."` (count of each letter separated by delimiter).

---

## Related Problems

- **Valid Anagram (LC 242)** — check if two strings are anagrams
- **Find All Anagrams (LC 438)** — find all anagram positions in a string
