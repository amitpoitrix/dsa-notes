# Satisfiability of Equality Equations — LC #990

**Pattern:** Union-Find (DSU)
**Difficulty:** Medium
**Companies:** Google · Amazon

---

## Problem

Given equations like `"a==b"`, `"b!=c"`, return whether all equations can be satisfied simultaneously.

```
Input:  ["a==b","b!=c","b==c"]
Output: false
```

---

## Intuition

Two-pass approach with DSU. First pass: process all `==` equations — union those variables together. Second pass: process all `!=` equations — if both variables have the same root, contradiction → return false.

---

## Algorithm

1. Initialize DSU for 26 characters (a-z).
2. First pass: for each `x==y`, union `x` and `y`.
3. Second pass: for each `x!=y`, if `find(x) == find(y)` → return false.
4. Return true.

---

## Code — Java

```java
public boolean equationsPossible(String[] equations) {
    int[] parent = new int[26];
    for (int i = 0; i < 26; i++) parent[i] = i;

    // first pass: union all equalities
    for (String eq : equations) {
        if (eq.charAt(1) == '=') {
            union(parent, eq.charAt(0) - 'a', eq.charAt(3) - 'a');
        }
    }

    // second pass: check inequalities
    for (String eq : equations) {
        if (eq.charAt(1) == '!') {
            if (find(parent, eq.charAt(0) - 'a') == find(parent, eq.charAt(3) - 'a')) {
                return false;
            }
        }
    }
    return true;
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
| Time  | O(n) | Two passes over equations, DSU ops near O(1) |
| Space | O(1) | Fixed 26-element array |

---

## Dry Run — ["a==b","b!=c","b==c"]

Pass 1 (==): union(a,b), union(b,c) → {a,b,c} all in same component.
Pass 2 (!=): b!=c → find(b)==find(c) → same root → **false**

---

## Edge Cases

- `"a!=a"` → find(a)==find(a) → false.
- All equalities, no inequalities → always true.

---

## Common Mistakes

- Processing `!=` before `==` — must do all equalities first to build full component picture.

---

## Related Problems

- **Redundant Connection (LC 684)** — basic DSU
- **Graph Valid Tree (LC 261)** — connectivity check
