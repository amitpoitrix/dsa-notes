# Accounts Merge — LC #721

**Pattern:** Union-Find (DSU)
**Difficulty:** Medium
**Companies:** Google · Facebook · Amazon

---

## Problem

Given a list of accounts where each account is `[name, email1, email2, ...]`, merge accounts that share at least one common email. Return merged accounts sorted.

```
Input:  [["John","a@a.com","b@b.com"],
         ["John","b@b.com","c@c.com"],
         ["Mary","d@d.com"]]
Output: [["John","a@a.com","b@b.com","c@c.com"],
         ["Mary","d@d.com"]]
```

---

## Intuition

Treat each email as a node. Emails in the same account → union them together. Use a HashMap to map each email to its account owner. After unioning, group emails by their root representative, sort each group, prepend the name.

---

## Algorithm

1. Create DSU for emails (map email → index).
2. For each account, union all emails to the first email in that account.
3. Also map each email → account name.
4. Group emails by `find(email)` root.
5. For each group: sort emails, prepend name, add to result.

---

## Code — Java

```java
public List<List<String>> accountsMerge(List<List<String>> accounts) {
    Map<String, String> parent = new HashMap<>();
    Map<String, String> emailToName = new HashMap<>();

    // initialize each email as its own parent
    for (List<String> account : accounts) {
        String name = account.get(0);
        for (int i = 1; i < account.size(); i++) {
            parent.put(account.get(i), account.get(i));
            emailToName.put(account.get(i), name);
        }
    }

    // union emails within same account
    for (List<String> account : accounts) {
        String first = account.get(1);
        for (int i = 2; i < account.size(); i++) {
            union(parent, first, account.get(i));
        }
    }

    // group by root
    Map<String, List<String>> groups = new HashMap<>();
    for (String email : parent.keySet()) {
        String root = find(parent, email);
        groups.computeIfAbsent(root, k -> new ArrayList<>()).add(email);
    }

    // build result
    List<List<String>> result = new ArrayList<>();
    for (Map.Entry<String, List<String>> entry : groups.entrySet()) {
        List<String> emails = entry.getValue();
        Collections.sort(emails);
        emails.add(0, emailToName.get(entry.getKey()));
        result.add(emails);
    }
    return result;
}

private String find(Map<String, String> parent, String x) {
    if (!parent.get(x).equals(x))
        parent.put(x, find(parent, parent.get(x)));
    return parent.get(x);
}

private void union(Map<String, String> parent, String x, String y) {
    String px = find(parent, x), py = find(parent, y);
    if (!px.equals(py)) parent.put(px, py);
}
```

---

## Complexity

| | Complexity | Reason |
|---|---|---|
| Time  | O(N K log(NK)) | N accounts, K emails each, sorting dominates |
| Space | O(NK) | HashMap storing all emails |

---

## Edge Cases

- Single account with one email — no merging needed.
- Same person, different names — problem guarantees name matches if accounts merge.
- All accounts completely separate — no merging, return as-is sorted.

---

## Common Mistakes

- Union the first email of each account as the representative — if you union randomly, tracking names becomes harder.
- Forgetting to sort emails within each merged group.

---

## Related Problems

- **Redundant Connection (LC 684)** — simpler DSU on integers
- **Smallest String With Swaps (LC 1202)** — same grouping-by-root pattern
- **Number of Islands (LC 200)** — DSU or DFS on grid
