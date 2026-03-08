# Min Stack — LC #155

**Pattern:** Stack with Auxiliary
**Difficulty:** Medium
**Companies:** Amazon · Google · Meta

---

## Problem

Design a stack that supports `push`, `pop`, `top`, and `getMin` in O(1).

---

## Intuition

Use two stacks: one main stack and one min stack. The min stack stores the current minimum at each level. When pushing, also push current min to min stack.

---

## Code — Java

```java
class MinStack {
    private Deque<Integer> stack = new ArrayDeque<>();
    private Deque<Integer> minStack = new ArrayDeque<>();

    public void push(int val) {
        stack.push(val);
        int min = minStack.isEmpty() ? val : Math.min(val, minStack.peek());
        minStack.push(min);
    }

    public void pop() {
        stack.pop();
        minStack.pop();
    }

    public int top() { return stack.peek(); }

    public int getMin() { return minStack.peek(); }
}
```

---

## Complexity

All operations O(1).

---

## Common Mistakes

- Storing only when new min found → incorrect, min stack size must match main stack.
