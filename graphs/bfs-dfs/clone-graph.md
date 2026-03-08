# Clone Graph — LC #133

**Pattern:** BFS + HashMap
**Difficulty:** Medium
**Companies:** Amazon · Meta · Google

---

## Problem

Deep copy a graph. Each node has a value and a list of neighbors.

---

## Code — Java (BFS)

```java
public Node cloneGraph(Node node) {
    if (node == null) return null;
    Map<Node, Node> map = new HashMap<>();
    Queue<Node> queue = new LinkedList<>();
    queue.offer(node);
    map.put(node, new Node(node.val));

    while (!queue.isEmpty()) {
        Node curr = queue.poll();
        for (Node neighbor : curr.neighbors) {
            if (!map.containsKey(neighbor)) {
                map.put(neighbor, new Node(neighbor.val));
                queue.offer(neighbor);
            }
            map.get(curr).neighbors.add(map.get(neighbor));
        }
    }
    return map.get(node);
}
```

---

## Complexity — O(n + e) time and space (n nodes, e edges)
