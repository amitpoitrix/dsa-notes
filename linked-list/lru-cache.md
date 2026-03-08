# LRU Cache — LC #146

**Pattern:** Doubly Linked List + HashMap
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta · Microsoft · Uber

---

## Problem

Design LRU (Least Recently Used) cache with `get` and `put` operations, both O(1).

---

## Intuition

HashMap gives O(1) lookup. Doubly linked list maintains order — most recently used at head, LRU at tail. On access/update, move node to head. On eviction, remove tail.

---

## Code — Java

```java
class LRUCache {
    private Map<Integer, Node> map;
    private Node head, tail; // dummy nodes
    private int capacity;

    class Node {
        int key, val;
        Node prev, next;
        Node(int k, int v) { key = k; val = v; }
    }

    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<>();
        head = new Node(0, 0); tail = new Node(0, 0);
        head.next = tail; tail.prev = head;
    }

    public int get(int key) {
        if (!map.containsKey(key)) return -1;
        Node node = map.get(key);
        remove(node);
        insertFront(node);
        return node.val;
    }

    public void put(int key, int value) {
        if (map.containsKey(key)) remove(map.get(key));
        Node node = new Node(key, value);
        insertFront(node);
        map.put(key, node);
        if (map.size() > capacity) {
            Node lru = tail.prev;
            remove(lru);
            map.remove(lru.key);
        }
    }

    private void remove(Node node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
    }

    private void insertFront(Node node) {
        node.next = head.next;
        node.prev = head;
        head.next.prev = node;
        head.next = node;
    }
}
```

---

## Complexity

Both `get` and `put` are O(1).

---

## Common Mistakes

- Using `LinkedHashMap` is the shortcut — correct but shows less depth.
- Forgetting to update the map when evicting.
