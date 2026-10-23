# Java for DSA — Refresher Notes

A quick-revision guide to Java basics and the Collections you'll use daily in DSA. Notes marked **Go →** point out where Java differs from what you're used to in Go.

---

## 1. Program Skeleton

```java
import java.util.*;
import java.io.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        System.out.println(n);
    }
}
```

**Go →** No `package main` + `func main()`. Everything lives inside a class. One `public` class per file, and the file name must match it.

### Fast I/O (for competitive problems)

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
StringTokenizer st = new StringTokenizer(br.readLine());
int n = Integer.parseInt(st.nextToken());

StringBuilder out = new StringBuilder();
out.append(n).append('\n');
System.out.print(out);
```

---

## 2. Primitive Types & Wrappers

| Primitive | Size | Range / Notes | Wrapper |
|---|---|---|---|
| `byte` | 8-bit | -128 to 127 | `Byte` |
| `short` | 16-bit | ~±32K | `Short` |
| `int` | 32-bit | ~±2.1 × 10⁹ | `Integer` |
| `long` | 64-bit | ~±9.2 × 10¹⁸ (suffix `L`) | `Long` |
| `float` | 32-bit | suffix `f` | `Float` |
| `double` | 64-bit | default decimal | `Double` |
| `char` | 16-bit | Unicode, `'a'` | `Character` |
| `boolean` | — | `true` / `false` | `Boolean` |

```java
Integer.MAX_VALUE;   // 2147483647
Integer.MIN_VALUE;   // -2147483648
Long.MAX_VALUE;
```

**Go →** `int` in Java is always 32-bit (Go's `int` is 64-bit on most machines). Use `long` when sums/products can exceed ~2 × 10⁹.

### Autoboxing gotcha ⚠️

Collections only hold objects, so `int` becomes `Integer` automatically.

```java
Integer a = 1000, b = 1000;
a == b;        // false!  (compares references)
a.equals(b);   // true    (compares values)
```

Always use `.equals()` when comparing values pulled out of collections.

### Overflow

```java
int mid = lo + (hi - lo) / 2;     // safe midpoint
long prod = (long) a * b;          // cast BEFORE multiplying
int MOD = 1_000_000_007;
```

---

## 3. Strings

Strings are **immutable**. Every `+` in a loop creates a new object — use `StringBuilder`.

```java
String s = "hello";
s.length();               // 5          (Go: len(s))
s.charAt(0);              // 'h'        (Go: s[0] gives a byte)
s.substring(1, 3);        // "el"       [start, end)
s.indexOf('l');           // 2
s.contains("ell");        // true
s.equals("hello");        // true — never use == for content
s.compareTo("world");     // negative (lexicographic)
s.toCharArray();          // char[]
s.split(" ");             // String[]
s.trim();
s.toUpperCase(); s.toLowerCase();
String.valueOf(42);       // "42"
Integer.parseInt("42");   // 42
String.join(",", list);
```

### StringBuilder

```java
StringBuilder sb = new StringBuilder();
sb.append("ab").append('c');
sb.insert(0, 'x');
sb.deleteCharAt(sb.length() - 1);
sb.reverse();
sb.setCharAt(0, 'z');
sb.toString();
```

### Character helpers

```java
Character.isDigit(c);
Character.isLetter(c);
Character.isLetterOrDigit(c);
Character.toLowerCase(c);
int idx = c - 'a';          // 0–25, for frequency arrays
char ch = (char) ('a' + 2); // 'c'
```

---

## 4. Arrays

```java
int[] arr = new int[n];               // zero-filled
int[] arr2 = {3, 1, 2};
int[][] grid = new int[rows][cols];
arr.length;                           // field, not a method

Arrays.fill(arr, -1);
Arrays.sort(arr);                     // ascending
Arrays.sort(arr, 1, 4);               // sort range [1, 4)
Arrays.toString(arr);                 // "[1, 2, 3]"  — for debugging
Arrays.deepToString(grid);
Arrays.copyOf(arr, newLen);
Arrays.copyOfRange(arr, 1, 3);
Arrays.equals(a, b);
Arrays.binarySearch(arr, key);        // array must be sorted
Arrays.stream(arr).sum();
Arrays.stream(arr).max().getAsInt();
```

**Go →** Arrays are fixed-size; there's no `append`. For a growable list use `ArrayList`.

### Sorting with a custom order

Primitive arrays can't take a comparator. Use the wrapper or a 2D array:

```java
Integer[] a = {3, 1, 2};
Arrays.sort(a, Collections.reverseOrder());      // descending

int[][] intervals = {{1, 3}, {0, 2}};
Arrays.sort(intervals, (x, y) -> x[0] - y[0]);   // by start
Arrays.sort(intervals, (x, y) -> Integer.compare(x[0], y[0])); // overflow-safe
```

---

## 5. Collections Framework — The Big Picture

```
Collection
├── List        → ArrayList, LinkedList
├── Set         → HashSet, LinkedHashSet, TreeSet
└── Queue       → LinkedList, PriorityQueue, ArrayDeque
    └── Deque   → ArrayDeque, LinkedList

Map (separate) → HashMap, LinkedHashMap, TreeMap
```

**Rule of thumb:** declare with the interface, instantiate with the implementation.

```java
List<Integer> list = new ArrayList<>();
Map<String, Integer> map = new HashMap<>();
```

---

## 6. List

### ArrayList — your default dynamic array (Go slice equivalent)

```java
List<Integer> list = new ArrayList<>();
list.add(5);                 // append           O(1) amortized
list.add(0, 10);             // insert at index  O(n)
list.get(i);                 //                  O(1)
list.set(i, 7);              //                  O(1)
list.remove(i);              // by index         O(n)
list.remove(Integer.valueOf(5)); // by value — careful with ints!
list.size();
list.isEmpty();
list.contains(5);            // O(n)
list.indexOf(5);
list.clear();

Collections.sort(list);
list.sort((a, b) -> b - a);  // descending
Collections.reverse(list);
Collections.max(list); Collections.min(list);
Collections.swap(list, i, j);

List<Integer> copy = new ArrayList<>(list);
List<Integer> fixed = Arrays.asList(1, 2, 3);   // fixed-size view
List<Integer> immut = List.of(1, 2, 3);         // immutable
```

⚠️ `list.remove(1)` removes **index 1**, not value 1. Use `list.remove(Integer.valueOf(1))` for value.

### List of lists (adjacency list, results)

```java
List<List<Integer>> adj = new ArrayList<>();
for (int i = 0; i < n; i++) adj.add(new ArrayList<>());
adj.get(u).add(v);

List<List<Integer>> res = new ArrayList<>();
res.add(new ArrayList<>(current));  // copy! (backtracking)
```

### LinkedList

Doubly linked. Rarely better than `ArrayList` for lists — mostly used as a `Queue`/`Deque`. Prefer `ArrayDeque` for those too.

---

## 7. Map

### HashMap — O(1) average

```java
Map<String, Integer> map = new HashMap<>();
map.put("a", 1);
map.get("a");                    // null if absent (Go: zero value + ok)
map.getOrDefault("b", 0);
map.containsKey("a");
map.containsValue(1);
map.remove("a");
map.size();
map.putIfAbsent("a", 0);

// Frequency counting — the classic
map.put(key, map.getOrDefault(key, 0) + 1);
map.merge(key, 1, Integer::sum);           // same thing, shorter

// Grouping
map.computeIfAbsent(key, k -> new ArrayList<>()).add(val);

// Iteration
for (Map.Entry<String, Integer> e : map.entrySet()) {
    e.getKey(); e.getValue();
}
for (String k : map.keySet()) { }
for (int v : map.values()) { }
```

**Go →** `v, ok := m[k]` becomes `map.containsKey(k)` / `map.get(k) != null`. `get` on a missing key returns `null`, and unboxing `null` into an `int` throws `NullPointerException`.

### LinkedHashMap

Keeps insertion order. Useful for LRU cache:

```java
new LinkedHashMap<>(cap, 0.75f, true) {   // true = access order
    protected boolean removeEldestEntry(Map.Entry<K, V> e) {
        return size() > cap;
    }
};
```

### TreeMap — sorted keys, O(log n)

```java
TreeMap<Integer, Integer> tm = new TreeMap<>();
tm.firstKey(); tm.lastKey();
tm.floorKey(x);      // greatest key ≤ x  (null if none)
tm.ceilingKey(x);    // smallest key ≥ x
tm.lowerKey(x);      // greatest key < x
tm.higherKey(x);     // smallest key > x
tm.pollFirstEntry(); tm.pollLastEntry();
tm.headMap(x);       // keys < x
tm.tailMap(x);       // keys ≥ x
tm.descendingMap();
```

Great for interval problems, calendar booking, sliding-window medians.

---

## 8. Set

```java
Set<Integer> set = new HashSet<>();       // O(1), unordered
set.add(x);          // returns false if already present
set.remove(x);
set.contains(x);
set.size();

Set<Integer> ordered = new LinkedHashSet<>(); // insertion order

TreeSet<Integer> ts = new TreeSet<>();    // sorted, O(log n)
ts.first(); ts.last();
ts.floor(x); ts.ceiling(x);
ts.lower(x); ts.higher(x);
ts.pollFirst(); ts.pollLast();
ts.headSet(x); ts.tailSet(x);

// Set operations
a.retainAll(b);   // intersection
a.addAll(b);      // union
a.removeAll(b);   // difference
```

**Go →** No more `map[int]struct{}` — Java has a real `Set`.

---

## 9. Stack, Queue, Deque

### Use `ArrayDeque` for both stack and queue

`Stack` class is legacy (synchronized, slower). Prefer `ArrayDeque`.

```java
// Stack (LIFO)
Deque<Integer> stack = new ArrayDeque<>();
stack.push(x);
stack.pop();
stack.peek();
stack.isEmpty();

// Queue (FIFO)
Queue<Integer> q = new ArrayDeque<>();
q.offer(x);          // add to tail
q.poll();            // remove head, null if empty
q.peek();            // view head, null if empty

// Deque (both ends) — sliding window max, 0-1 BFS
Deque<Integer> dq = new ArrayDeque<>();
dq.offerFirst(x); dq.offerLast(x);
dq.pollFirst();   dq.pollLast();
dq.peekFirst();   dq.peekLast();
```

| Throws on failure | Returns null/false |
|---|---|
| `add` | `offer` |
| `remove` | `poll` |
| `element` | `peek` |

Stick to the right column in DSA.

⚠️ `ArrayDeque` does not allow `null` elements.

---

## 10. PriorityQueue (Heap)

Min-heap by default. `offer`/`poll` are O(log n), `peek` is O(1).

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
PriorityQueue<Integer> maxHeap2 = new PriorityQueue<>((a, b) -> b - a);

minHeap.offer(5);
minHeap.peek();
minHeap.poll();
minHeap.size();

// Heap of arrays — Dijkstra: {node, dist}
PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
pq.offer(new int[]{src, 0});

// Top K frequent: min-heap of size k
PriorityQueue<Map.Entry<Integer, Integer>> heap =
    new PriorityQueue<>((a, b) -> a.getValue() - b.getValue());
```

**Go →** No need to implement `heap.Interface` with `Len/Less/Swap/Push/Pop`. Huge time saver.

⚠️ Iterating a `PriorityQueue` with a for-each does **not** give sorted order — only `poll()` does.

---

## 11. Comparators

```java
// Lambda
(a, b) -> a - b              // ascending (may overflow for large values)
(a, b) -> Integer.compare(a, b)  // safe

// Comparator helpers
Comparator.comparingInt(x -> x[0])
Comparator.comparingInt((int[] x) -> x[0]).thenComparingInt(x -> x[1])
Comparator.comparing(String::length).reversed()

// Custom class
class Pair implements Comparable<Pair> {
    int first, second;
    Pair(int f, int s) { first = f; second = s; }
    public int compareTo(Pair o) {
        return Integer.compare(this.first, o.first);
    }
}
```

Return negative → `a` comes first, positive → `b` comes first, 0 → equal.

---

## 12. Custom Classes for DSA

```java
// Linked list node
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
}

// Binary tree node
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

// Graph edge
record Edge(int to, int weight) {}   // Java 16+, gives equals/hashCode for free
```

### Using objects as HashMap keys

Override **both** `equals` and `hashCode`, or use a `record`, or encode as a string/long:

```java
String key = r + "," + c;
long key = (long) r * cols + c;
```

**Go →** Go structs are comparable map keys by default; Java classes are not (they compare by reference) unless you override these methods.

---

## 13. Pass-by-Value Reminder

Java is always pass-by-value, but object variables hold **references**.

- Modifying a list/array inside a method → visible to caller.
- Reassigning the parameter (`list = new ArrayList<>()`) → not visible.
- Primitives can't be changed by a method. For a "global counter" in recursion, use a class field or `int[] count = {0}`.

**Go →** Similar to passing a slice/map in Go (shared underlying data), but there are no pointers to primitives.

---

## 14. Useful Utilities

```java
Math.max(a, b); Math.min(a, b);
Math.abs(x);
Math.pow(2, 10);      // returns double
Math.sqrt(x);
Math.floorMod(a, m);  // always non-negative

Integer.bitCount(x);              // number of 1 bits
Integer.toBinaryString(x);
Integer.highestOneBit(x);
Integer.numberOfTrailingZeros(x);

Collections.frequency(list, x);
Collections.unmodifiableList(list);
Collections.nCopies(n, 0);
```

### Bit tricks

```java
x & 1          // odd check
x >> 1         // divide by 2
x << 1         // multiply by 2
x & (x - 1)    // remove lowest set bit
x & -x         // isolate lowest set bit
(mask >> i) & 1  // i-th bit
mask | (1 << i)  // set i-th bit
```

---

## 15. Time Complexity Cheat Sheet

| Structure | Access | Search | Insert | Delete |
|---|---|---|---|---|
| Array | O(1) | O(n) | — | — |
| ArrayList | O(1) | O(n) | O(1)* end / O(n) mid | O(n) |
| LinkedList | O(n) | O(n) | O(1) ends | O(1) ends |
| HashMap / HashSet | — | O(1) avg | O(1) avg | O(1) avg |
| TreeMap / TreeSet | — | O(log n) | O(log n) | O(log n) |
| PriorityQueue | O(1) peek | O(n) | O(log n) | O(log n) poll |
| ArrayDeque | O(1) ends | O(n) | O(1) ends | O(1) ends |

`Arrays.sort` on primitives: dual-pivot quicksort, O(n log n) average.
`Collections.sort` / object arrays: TimSort, O(n log n), stable.

---

## 16. Which Collection for Which Pattern

| Pattern / Problem | Go-to Structure |
|---|---|
| Frequency count, two-sum | `HashMap` |
| Seen / visited / duplicates | `HashSet` or `boolean[]` |
| Sliding window max/min | `ArrayDeque` (monotonic deque) |
| Next greater element, valid parentheses | `ArrayDeque` as stack |
| BFS, level-order traversal | `ArrayDeque` as queue |
| Top K, K-th largest, merge K lists | `PriorityQueue` |
| Dijkstra, Prim | `PriorityQueue<int[]>` |
| Running median | Two `PriorityQueue`s |
| Floor/ceiling lookups, intervals | `TreeMap` / `TreeSet` |
| LRU cache | `LinkedHashMap` or `HashMap` + doubly linked list |
| Graph adjacency | `List<List<Integer>>` |
| Grouping (anagrams) | `HashMap<String, List<String>>` |
| Union-Find | `int[] parent, rank` |
| Trie | Custom node with `TreeNode[26]` or `HashMap<Character, Node>` |

---

## 17. Common Templates

### BFS on a grid

```java
int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
Queue<int[]> q = new ArrayDeque<>();
boolean[][] seen = new boolean[m][n];
q.offer(new int[]{sr, sc});
seen[sr][sc] = true;

while (!q.isEmpty()) {
    int[] cur = q.poll();
    for (int[] d : dirs) {
        int r = cur[0] + d[0], c = cur[1] + d[1];
        if (r < 0 || c < 0 || r >= m || c >= n || seen[r][c]) continue;
        seen[r][c] = true;
        q.offer(new int[]{r, c});
    }
}
```

### Binary search (lower bound)

```java
int lo = 0, hi = n;
while (lo < hi) {
    int mid = lo + (hi - lo) / 2;
    if (arr[mid] < target) lo = mid + 1;
    else hi = mid;
}
// lo = first index with arr[lo] >= target
```

### Backtracking

```java
void backtrack(List<List<Integer>> res, List<Integer> cur, int[] nums, int start) {
    res.add(new ArrayList<>(cur));
    for (int i = start; i < nums.length; i++) {
        cur.add(nums[i]);
        backtrack(res, cur, nums, i + 1);
        cur.remove(cur.size() - 1);
    }
}
```

### Union-Find

```java
int[] parent = new int[n];
for (int i = 0; i < n; i++) parent[i] = i;

int find(int x) {
    if (parent[x] != x) parent[x] = find(parent[x]);
    return parent[x];
}
void union(int a, int b) { parent[find(a)] = find(b); }
```

### Memoized DP

```java
int[] memo = new int[n + 1];
Arrays.fill(memo, -1);

int dp(int i) {
    if (i <= 1) return i;
    if (memo[i] != -1) return memo[i];
    return memo[i] = dp(i - 1) + dp(i - 2);
}
```

---

## 18. Go → Java Quick Translation

| Go | Java |
|---|---|
| `s := []int{}` | `List<Integer> s = new ArrayList<>();` |
| `s = append(s, x)` | `s.add(x);` |
| `len(s)` | `s.size()` / `arr.length` / `str.length()` |
| `m := map[string]int{}` | `Map<String,Integer> m = new HashMap<>();` |
| `v, ok := m[k]` | `m.containsKey(k)` / `m.getOrDefault(k, 0)` |
| `delete(m, k)` | `m.remove(k);` |
| `map[int]struct{}` | `Set<Integer> set = new HashSet<>();` |
| `sort.Ints(a)` | `Arrays.sort(a);` |
| `sort.Slice(a, less)` | `list.sort((x, y) -> ...);` |
| `container/heap` | `PriorityQueue` |
| `for i, v := range s` | `for (int i = 0; i < s.size(); i++)` / `for (int v : s)` |
| `math.MaxInt64` | `Long.MAX_VALUE` |
| `strings.Builder` | `StringBuilder` |
| `nil` | `null` |
| multiple return values | return `int[]`, a `record`, or a small class |

---

## 19. Common Pitfalls Checklist

- Comparing `Integer`/`String` with `==` instead of `.equals()`
- `list.remove(int)` removing by index instead of value
- `int` overflow — use `long` for sums, products, and `(long) a * b`
- `a - b` comparator overflowing — use `Integer.compare`
-  Unboxing `null` from `map.get()` → `NullPointerException`
-  Adding the same list reference to results in backtracking (always copy)
-  Using `Stack` instead of `ArrayDeque`
-  String concatenation in a loop instead of `StringBuilder`
-  Expecting sorted order while iterating a `PriorityQueue`
-  Forgetting `hashCode`/`equals` on custom key classes
