# Smallest String With Swaps — LC #1202

**Pattern:** Union-Find (DSU)
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Given string `s` and list of pairs `pairs` where you can swap characters at those indices any number of times, return the lexicographically smallest string.

```
Input:  s = "dcab", pairs = [[0,3],[1,2]]
Output: "bacd"
```

---

## Intuition

If indices are connected (directly or transitively through pairs), you can arrange their characters in any order. Use DSU to group connected indices together, sort characters in each group, place them back in sorted order.

---

## Algorithm

1. Build DSU over indices 0 to n-1.
2. For each pair `[i, j]`, union `i` and `j`.
3. Group indices by their root: `root → [indices]`.
4. For each group: collect characters, sort them, place back by sorted index order.

---

## Code — Java

```java
public String smallestStringWithSwaps(String s, List<List<Integer>> pairs) {
    int n = s.length();
    int[] parent = new int[n];
    for (int i = 0; i < n; i++) parent[i] = i;

    for (List<Integer> pair : pairs) {
        union(parent, pair.get(0), pair.get(1));
    }

    // group indices by root
    Map<Integer, List<Integer>> groups = new HashMap<>();
    for (int i = 0; i < n; i++) {
        int root = find(parent, i);
        groups.computeIfAbsent(root, k -> new ArrayList<>()).add(i);
    }

    char[] result = new char[n];
    for (List<Integer> indices : groups.values()) {
        // collect chars, sort both
        List<Character> chars = new ArrayList<>();
        for (int idx : indices) chars.add(s.charAt(idx));
        Collections.sort(indices);
        Collections.sort(chars);
        // place smallest chars at smallest indices
        for (int i = 0; i < indices.size(); i++) {
            result[indices.get(i)] = chars.get(i);
        }
    }
    return new String(result);
}

private int find(int[] parent, int x) {
    if (parent[x] != x) parent[x] = find(parent, parent[x]);
    return parent[x];
}

private void union(int[] parent, int x, int y) {
    int px = find(parent, x), py = find(parent, y);
    if (px != py) parent[px] = py;
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(n log n) | Sorting characters per group |
| Space | O(n) | DSU + group map |

---

## Edge Cases

- No pairs → return `s` unchanged.
- All indices connected → sort the entire string.

---

## Common Mistakes

- Sorting indices and chars independently — must sort both and pair them together (smallest char → smallest index).

---

## Related Problems

- **Accounts Merge (LC 721)** — same group-by-root pattern with strings
- **Redundant Connection (LC 684)** — basic DSU
