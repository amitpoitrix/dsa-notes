# DSA Notes

Interview prep notes for top product-based companies.
Each file covers: Problem → Intuition → Algorithm → Java Code → Complexity → Dry Run → Edge Cases → Mistakes → Related Problems.

**Language:** Java
**Target:** Google · Meta · Amazon · Microsoft · Uber · Flipkart

---

## Progress Tracker

| Pattern | Problems | Status |
|---|---|---|
| Two Pointers | 8 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Sliding Window | 8 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Prefix Sum | 6 | 🔲 🔲 🔲 🔲 🔲 🔲 |
| Hashing | 8 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Binary Search | 9 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Kadane's | 5 | 🔲 🔲 🔲 🔲 🔲 |
| Monotonic Stack | 12 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Sorting & Greedy | 6 | 🔲 🔲 🔲 🔲 🔲 🔲 |
| Cyclic Sort | 5 | 🔲 🔲 🔲 🔲 🔲 |
| Linked List | 12 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Tree DFS | 16 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Tree BFS | 8 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| BST | 6 | 🔲 🔲 🔲 🔲 🔲 🔲 |
| Graph BFS/DFS | 12 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Topological Sort | 7 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Shortest Path | 7 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Union Find | 7 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Heap | 11 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Backtracking | 12 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| Trie | 7 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| DP 1D | 9 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| DP 2D/Grid | 6 | 🔲 🔲 🔲 🔲 🔲 🔲 |
| DP Knapsack | 5 | 🔲 🔲 🔲 🔲 🔲 |
| DP LCS/Strings | 7 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |
| DP LIS | 5 | 🔲 🔲 🔲 🔲 🔲 |
| DP Intervals | 5 | 🔲 🔲 🔲 🔲 🔲 |
| DP State Machine | 4 | 🔲 🔲 🔲 🔲 |
| Bit Manipulation | 10 | 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 🔲 |

---

## Arrays & Strings

### Two Pointers
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Two Sum II | 167 | Easy | [notes](arrays-strings/two-pointers/two-sum-ii.md) |
| 2 | 3Sum | 15 | Medium | [notes](arrays-strings/two-pointers/3sum.md) |
| 3 | 3Sum Closest | 16 | Medium | [notes](arrays-strings/two-pointers/3sum-closest.md) |
| 4 | Container With Most Water | 11 | Medium | [notes](arrays-strings/two-pointers/container-with-most-water.md) |
| 5 | Trapping Rain Water | 42 | Hard | [notes](arrays-strings/two-pointers/trapping-rain-water.md) |
| 6 | Valid Palindrome | 125 | Easy | [notes](arrays-strings/two-pointers/valid-palindrome.md) |
| 7 | Remove Duplicates from Sorted Array | 26 | Easy | [notes](arrays-strings/two-pointers/remove-duplicates.md) |
| 8 | Sort Colors | 75 | Medium | [notes](arrays-strings/two-pointers/sort-colors.md) |

### Sliding Window
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Maximum Sum Subarray of Size K | — | Easy | [notes](arrays-strings/sliding-window/max-sum-subarray-k.md) |
| 2 | Longest Substring Without Repeating Characters | 3 | Medium | [notes](arrays-strings/sliding-window/longest-substring-no-repeat.md) |
| 3 | Longest Substring with At Most K Distinct Characters | 340 | Medium | [notes](arrays-strings/sliding-window/longest-k-distinct.md) |
| 4 | Minimum Window Substring | 76 | Hard | [notes](arrays-strings/sliding-window/minimum-window-substring.md) |
| 5 | Find All Anagrams in a String | 438 | Medium | [notes](arrays-strings/sliding-window/find-all-anagrams.md) |
| 6 | Permutation in String | 567 | Medium | [notes](arrays-strings/sliding-window/permutation-in-string.md) |
| 7 | Fruits Into Baskets | 904 | Medium | [notes](arrays-strings/sliding-window/fruits-into-baskets.md) |
| 8 | Max Consecutive Ones III | 1004 | Medium | [notes](arrays-strings/sliding-window/max-consecutive-ones-iii.md) |

### Prefix Sum
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Subarray Sum Equals K | 560 | Medium | [notes](arrays-strings/prefix-sum/subarray-sum-equals-k.md) |
| 2 | Product of Array Except Self | 238 | Medium | [notes](arrays-strings/prefix-sum/product-except-self.md) |
| 3 | Range Sum Query | 303 | Easy | [notes](arrays-strings/prefix-sum/range-sum-query.md) |
| 4 | Contiguous Array | 525 | Medium | [notes](arrays-strings/prefix-sum/contiguous-array.md) |
| 5 | Minimum Size Subarray Sum | 209 | Medium | [notes](arrays-strings/prefix-sum/minimum-size-subarray-sum.md) |
| 6 | Number of Subarrays with Bounded Maximum | 795 | Medium | [notes](arrays-strings/prefix-sum/subarrays-bounded-max.md) |

### Hashing
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Two Sum | 1 | Easy | [notes](arrays-strings/hashing/two-sum.md) |
| 2 | Group Anagrams | 49 | Medium | [notes](arrays-strings/hashing/group-anagrams.md) |
| 3 | Top K Frequent Elements | 347 | Medium | [notes](arrays-strings/hashing/top-k-frequent.md) |
| 4 | Longest Consecutive Sequence | 128 | Medium | [notes](arrays-strings/hashing/longest-consecutive.md) |
| 5 | Valid Anagram | 242 | Easy | [notes](arrays-strings/hashing/valid-anagram.md) |
| 6 | First Non-Repeating Character | 387 | Easy | [notes](arrays-strings/hashing/first-non-repeating-char.md) |
| 7 | 4Sum II | 454 | Medium | [notes](arrays-strings/hashing/4sum-ii.md) |
| 8 | Subarray with Zero Sum | — | Easy | [notes](arrays-strings/hashing/subarray-zero-sum.md) |

### Binary Search
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Binary Search | 704 | Easy | [notes](arrays-strings/binary-search/binary-search.md) |
| 2 | Search in Rotated Sorted Array | 33 | Medium | [notes](arrays-strings/binary-search/search-rotated-array.md) |
| 3 | Find Minimum in Rotated Sorted Array | 153 | Medium | [notes](arrays-strings/binary-search/find-min-rotated.md) |
| 4 | Median of Two Sorted Arrays | 4 | Hard | [notes](arrays-strings/binary-search/median-two-sorted-arrays.md) |
| 5 | Koko Eating Bananas | 875 | Medium | [notes](arrays-strings/binary-search/koko-eating-bananas.md) |
| 6 | Capacity to Ship Packages | 1011 | Medium | [notes](arrays-strings/binary-search/capacity-ship-packages.md) |
| 7 | Split Array Largest Sum | 410 | Hard | [notes](arrays-strings/binary-search/split-array-largest-sum.md) |
| 8 | Find K Closest Elements | 658 | Medium | [notes](arrays-strings/binary-search/k-closest-elements.md) |
| 9 | Find Peak Element | 162 | Medium | [notes](arrays-strings/binary-search/find-peak-element.md) |

### Kadane's Algorithm
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Maximum Subarray | 53 | Medium | [notes](arrays-strings/kadanes/maximum-subarray.md) |
| 2 | Maximum Product Subarray | 152 | Medium | [notes](arrays-strings/kadanes/maximum-product-subarray.md) |
| 3 | Best Time to Buy and Sell Stock | 121 | Easy | [notes](arrays-strings/kadanes/best-time-buy-sell.md) |
| 4 | Best Time to Buy and Sell Stock II | 122 | Medium | [notes](arrays-strings/kadanes/best-time-buy-sell-ii.md) |
| 5 | Maximum Sum Circular Subarray | 918 | Medium | [notes](arrays-strings/kadanes/max-sum-circular-subarray.md) |

### Monotonic Stack
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Valid Parentheses | 20 | Easy | [notes](arrays-strings/monotonic-stack/valid-parentheses.md) |
| 2 | Min Stack | 155 | Medium | [notes](arrays-strings/monotonic-stack/min-stack.md) |
| 3 | Daily Temperatures | 739 | Medium | [notes](arrays-strings/monotonic-stack/daily-temperatures.md) |
| 4 | Next Greater Element I & II | 496/503 | Medium | [notes](arrays-strings/monotonic-stack/next-greater-element.md) |
| 5 | Largest Rectangle in Histogram | 84 | Hard | [notes](arrays-strings/monotonic-stack/largest-rectangle-histogram.md) |
| 6 | Remove K Digits | 402 | Medium | [notes](arrays-strings/monotonic-stack/remove-k-digits.md) |
| 7 | Sum of Subarray Minimums | 907 | Medium | [notes](arrays-strings/monotonic-stack/sum-subarray-minimums.md) |
| 8 | 132 Pattern | 456 | Medium | [notes](arrays-strings/monotonic-stack/132-pattern.md) |

### Sorting & Greedy
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Merge Intervals | 56 | Medium | [notes](arrays-strings/sorting-greedy/merge-intervals.md) |
| 2 | Insert Interval | 57 | Medium | [notes](arrays-strings/sorting-greedy/insert-interval.md) |
| 3 | Non-overlapping Intervals | 435 | Medium | [notes](arrays-strings/sorting-greedy/non-overlapping-intervals.md) |
| 4 | Meeting Rooms II | 253 | Medium | [notes](arrays-strings/sorting-greedy/meeting-rooms-ii.md) |
| 5 | Largest Number | 179 | Medium | [notes](arrays-strings/sorting-greedy/largest-number.md) |
| 6 | Minimum Arrows to Burst Balloons | 452 | Medium | [notes](arrays-strings/sorting-greedy/minimum-arrows-balloons.md) |

### Cyclic Sort
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Missing Number | 268 | Easy | [notes](arrays-strings/cyclic-sort/missing-number.md) |
| 2 | Find All Duplicates | 442 | Medium | [notes](arrays-strings/cyclic-sort/find-all-duplicates.md) |
| 3 | First Missing Positive | 41 | Hard | [notes](arrays-strings/cyclic-sort/first-missing-positive.md) |
| 4 | Find the Duplicate Number | 287 | Medium | [notes](arrays-strings/cyclic-sort/find-duplicate-number.md) |
| 5 | Set Mismatch | 645 | Easy | [notes](arrays-strings/cyclic-sort/set-mismatch.md) |

---

## Linked List
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Reverse Linked List | 206 | Easy | [notes](linked-list/reverse-linked-list.md) |
| 2 | Reverse in K-Groups | 25 | Hard | [notes](linked-list/reverse-k-groups.md) |
| 3 | Merge Two Sorted Lists | 21 | Easy | [notes](linked-list/merge-two-sorted-lists.md) |
| 4 | Merge K Sorted Lists | 23 | Hard | [notes](linked-list/merge-k-sorted-lists.md) |
| 5 | Linked List Cycle | 141 | Easy | [notes](linked-list/linked-list-cycle.md) |
| 6 | Find Middle of Linked List | 876 | Easy | [notes](linked-list/find-middle.md) |
| 7 | Remove Nth Node From End | 19 | Medium | [notes](linked-list/remove-nth-from-end.md) |
| 8 | Copy List with Random Pointer | 138 | Medium | [notes](linked-list/copy-list-random-pointer.md) |
| 9 | LRU Cache | 146 | Medium | [notes](linked-list/lru-cache.md) |
| 10 | Reorder List | 143 | Medium | [notes](linked-list/reorder-list.md) |
| 11 | Add Two Numbers | 2 | Medium | [notes](linked-list/add-two-numbers.md) |
| 12 | Sort List | 148 | Medium | [notes](linked-list/sort-list.md) |

---

## Trees

### DFS
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Maximum Depth of Binary Tree | 104 | Easy | [notes](trees/dfs/max-depth.md) |
| 2 | Diameter of Binary Tree | 543 | Easy | [notes](trees/dfs/diameter.md) |
| 3 | Binary Tree Maximum Path Sum | 124 | Hard | [notes](trees/dfs/max-path-sum.md) |
| 4 | Lowest Common Ancestor | 236 | Medium | [notes](trees/dfs/lowest-common-ancestor.md) |
| 5 | Path Sum II | 113 | Medium | [notes](trees/dfs/path-sum-ii.md) |
| 6 | Path Sum III | 437 | Medium | [notes](trees/dfs/path-sum-iii.md) |
| 7 | Flatten Binary Tree to Linked List | 114 | Medium | [notes](trees/dfs/flatten-to-linked-list.md) |
| 8 | Invert Binary Tree | 226 | Easy | [notes](trees/dfs/invert-binary-tree.md) |
| 9 | Symmetric Tree | 101 | Easy | [notes](trees/dfs/symmetric-tree.md) |
| 10 | Count Good Nodes | 1448 | Medium | [notes](trees/dfs/count-good-nodes.md) |
| 11 | Validate BST | 98 | Medium | [notes](trees/dfs/validate-bst.md) |
| 12 | Kth Smallest in BST | 230 | Medium | [notes](trees/dfs/kth-smallest-bst.md) |
| 13 | Construct BT from Preorder + Inorder | 105 | Medium | [notes](trees/dfs/construct-from-preorder-inorder.md) |
| 14 | Serialize and Deserialize BT | 297 | Hard | [notes](trees/dfs/serialize-deserialize.md) |

### BFS
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Binary Tree Level Order Traversal | 102 | Medium | [notes](trees/bfs/level-order-traversal.md) |
| 2 | Binary Tree Zigzag Level Order | 103 | Medium | [notes](trees/bfs/zigzag-level-order.md) |
| 3 | Right Side View | 199 | Medium | [notes](trees/bfs/right-side-view.md) |
| 4 | Average of Levels | 637 | Easy | [notes](trees/bfs/average-of-levels.md) |
| 5 | Minimum Depth | 111 | Easy | [notes](trees/bfs/minimum-depth.md) |
| 6 | Populating Next Right Pointers | 116 | Medium | [notes](trees/bfs/next-right-pointers.md) |
| 7 | Vertical Order Traversal | 987 | Hard | [notes](trees/bfs/vertical-order-traversal.md) |

### BST
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Insert / Delete in BST | 450 | Medium | [notes](trees/bst/insert-delete-bst.md) |
| 2 | Search in BST | 700 | Easy | [notes](trees/bst/search-bst.md) |
| 3 | Recover BST | 99 | Hard | [notes](trees/bst/recover-bst.md) |
| 4 | BST Iterator | 173 | Medium | [notes](trees/bst/bst-iterator.md) |
| 5 | Convert Sorted Array to BST | 108 | Easy | [notes](trees/bst/sorted-array-to-bst.md) |

---

## Graphs

### BFS / DFS
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Number of Islands | 200 | Medium | [notes](graphs/bfs-dfs/number-of-islands.md) |
| 2 | Clone Graph | 133 | Medium | [notes](graphs/bfs-dfs/clone-graph.md) |
| 3 | Word Ladder | 127 | Hard | [notes](graphs/bfs-dfs/word-ladder.md) |
| 4 | Rotting Oranges | 994 | Medium | [notes](graphs/bfs-dfs/rotting-oranges.md) |
| 5 | Pacific Atlantic Water Flow | 417 | Medium | [notes](graphs/bfs-dfs/pacific-atlantic.md) |
| 6 | Surrounded Regions | 130 | Medium | [notes](graphs/bfs-dfs/surrounded-regions.md) |
| 7 | Max Area of Island | 695 | Medium | [notes](graphs/bfs-dfs/max-area-island.md) |
| 8 | Number of Connected Components | 323 | Medium | [notes](graphs/bfs-dfs/connected-components.md) |
| 9 | Is Graph Bipartite | 785 | Medium | [notes](graphs/bfs-dfs/is-bipartite.md) |
| 10 | Shortest Path in Binary Matrix | 1091 | Medium | [notes](graphs/bfs-dfs/shortest-path-binary-matrix.md) |

### Topological Sort
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Course Schedule I | 207 | Medium | [notes](graphs/topological-sort/course-schedule-i.md) |
| 2 | Course Schedule II | 210 | Medium | [notes](graphs/topological-sort/course-schedule-ii.md) |
| 3 | Alien Dictionary | 269 | Hard | [notes](graphs/topological-sort/alien-dictionary.md) |
| 4 | Minimum Height Trees | 310 | Medium | [notes](graphs/topological-sort/minimum-height-trees.md) |
| 5 | Sequence Reconstruction | 444 | Medium | [notes](graphs/topological-sort/sequence-reconstruction.md) |
| 6 | Parallel Courses | 1136 | Medium | [notes](graphs/topological-sort/parallel-courses.md) |

### Shortest Path
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Network Delay Time | 743 | Medium | [notes](graphs/shortest-path/network-delay-time.md) |
| 2 | Cheapest Flights Within K Stops | 787 | Medium | [notes](graphs/shortest-path/cheapest-flights.md) |
| 3 | Path With Minimum Effort | 1631 | Medium | [notes](graphs/shortest-path/min-effort-path.md) |
| 4 | Find the City With Smallest Neighbors | 1334 | Medium | [notes](graphs/shortest-path/city-smallest-neighbors.md) |
| 5 | Minimum Cost to Connect All Points | 1584 | Medium | [notes](graphs/shortest-path/min-cost-connect-points.md) |
| 6 | Critical Connections | 1192 | Hard | [notes](graphs/shortest-path/critical-connections.md) |

### Union Find
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Redundant Connection | 684 | Medium | [notes](graphs/union-find/redundant-connection.md) |
| 2 | Graph Valid Tree | 261 | Medium | [notes](graphs/union-find/graph-valid-tree.md) |
| 3 | Accounts Merge | 721 | Medium | [notes](graphs/union-find/accounts-merge.md) |
| 4 | Smallest String With Swaps | 1202 | Medium | [notes](graphs/union-find/smallest-string-swaps.md) |
| 5 | Satisfiability of Equality Equations | 990 | Medium | [notes](graphs/union-find/equality-equations.md) |
| 6 | Making a Large Island | 827 | Hard | [notes](graphs/union-find/making-large-island.md) |

---

## Heap / Priority Queue
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Kth Largest Element in Array | 215 | Medium | [notes](heap/kth-largest-element.md) |
| 2 | Top K Frequent Elements | 347 | Medium | [notes](heap/top-k-frequent.md) |
| 3 | K Closest Points to Origin | 973 | Medium | [notes](heap/k-closest-points.md) |
| 4 | Find Median from Data Stream | 295 | Hard | [notes](heap/find-median-data-stream.md) |
| 5 | Merge K Sorted Lists | 23 | Hard | [notes](heap/merge-k-sorted-lists.md) |
| 6 | Task Scheduler | 621 | Medium | [notes](heap/task-scheduler.md) |
| 7 | Reorganize String | 767 | Medium | [notes](heap/reorganize-string.md) |
| 8 | Meeting Rooms II | 253 | Medium | [notes](heap/meeting-rooms-ii.md) |
| 9 | Smallest Range Covering K Lists | 632 | Hard | [notes](heap/smallest-range-k-lists.md) |

---

## Backtracking
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Subsets | 78 | Medium | [notes](backtracking/subsets.md) |
| 2 | Subsets II | 90 | Medium | [notes](backtracking/subsets-ii.md) |
| 3 | Permutations | 46 | Medium | [notes](backtracking/permutations.md) |
| 4 | Permutations II | 47 | Medium | [notes](backtracking/permutations-ii.md) |
| 5 | Combination Sum | 39 | Medium | [notes](backtracking/combination-sum.md) |
| 6 | Combination Sum II | 40 | Medium | [notes](backtracking/combination-sum-ii.md) |
| 7 | Letter Combinations of Phone Number | 17 | Medium | [notes](backtracking/letter-combinations.md) |
| 8 | Word Search | 79 | Medium | [notes](backtracking/word-search.md) |
| 9 | N-Queens | 51 | Hard | [notes](backtracking/n-queens.md) |
| 10 | Sudoku Solver | 37 | Hard | [notes](backtracking/sudoku-solver.md) |
| 11 | Palindrome Partitioning | 131 | Medium | [notes](backtracking/palindrome-partitioning.md) |
| 12 | Generate Parentheses | 22 | Medium | [notes](backtracking/generate-parentheses.md) |

---

## Trie
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Implement Trie | 208 | Medium | [notes](trie/implement-trie.md) |
| 2 | Design Add & Search Words | 211 | Medium | [notes](trie/add-search-words.md) |
| 3 | Word Search II | 212 | Hard | [notes](trie/word-search-ii.md) |
| 4 | Replace Words | 648 | Medium | [notes](trie/replace-words.md) |
| 5 | Longest Word in Dictionary | 720 | Medium | [notes](trie/longest-word-dictionary.md) |
| 6 | Map Sum Pairs | 677 | Medium | [notes](trie/map-sum-pairs.md) |

---

## Dynamic Programming

### 1D DP
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Climbing Stairs | 70 | Easy | [notes](dynamic-programming/1d/climbing-stairs.md) |
| 2 | House Robber | 198 | Medium | [notes](dynamic-programming/1d/house-robber.md) |
| 3 | House Robber II | 213 | Medium | [notes](dynamic-programming/1d/house-robber-ii.md) |
| 4 | Jump Game | 55 | Medium | [notes](dynamic-programming/1d/jump-game.md) |
| 5 | Jump Game II | 45 | Medium | [notes](dynamic-programming/1d/jump-game-ii.md) |
| 6 | Decode Ways | 91 | Medium | [notes](dynamic-programming/1d/decode-ways.md) |
| 7 | Word Break | 139 | Medium | [notes](dynamic-programming/1d/word-break.md) |
| 8 | Coin Change | 322 | Medium | [notes](dynamic-programming/1d/coin-change.md) |
| 9 | Coin Change II | 518 | Medium | [notes](dynamic-programming/1d/coin-change-ii.md) |

### 2D / Grid DP
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Unique Paths | 62 | Medium | [notes](dynamic-programming/2d-grid/unique-paths.md) |
| 2 | Unique Paths II | 63 | Medium | [notes](dynamic-programming/2d-grid/unique-paths-ii.md) |
| 3 | Minimum Path Sum | 64 | Medium | [notes](dynamic-programming/2d-grid/minimum-path-sum.md) |
| 4 | Triangle | 120 | Medium | [notes](dynamic-programming/2d-grid/triangle.md) |
| 5 | Maximal Square | 221 | Medium | [notes](dynamic-programming/2d-grid/maximal-square.md) |
| 6 | Dungeon Game | 174 | Hard | [notes](dynamic-programming/2d-grid/dungeon-game.md) |

### Knapsack
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Partition Equal Subset Sum | 416 | Medium | [notes](dynamic-programming/knapsack/partition-equal-subset.md) |
| 2 | Last Stone Weight II | 1049 | Medium | [notes](dynamic-programming/knapsack/last-stone-weight-ii.md) |
| 3 | Target Sum | 494 | Medium | [notes](dynamic-programming/knapsack/target-sum.md) |
| 4 | Ones and Zeroes | 474 | Medium | [notes](dynamic-programming/knapsack/ones-and-zeroes.md) |

### LCS / Strings
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Longest Common Subsequence | 1143 | Medium | [notes](dynamic-programming/lcs-strings/longest-common-subsequence.md) |
| 2 | Edit Distance | 72 | Hard | [notes](dynamic-programming/lcs-strings/edit-distance.md) |
| 3 | Shortest Common Supersequence | 1092 | Hard | [notes](dynamic-programming/lcs-strings/shortest-common-supersequence.md) |
| 4 | Distinct Subsequences | 115 | Hard | [notes](dynamic-programming/lcs-strings/distinct-subsequences.md) |
| 5 | Wildcard Matching | 44 | Hard | [notes](dynamic-programming/lcs-strings/wildcard-matching.md) |
| 6 | Regular Expression Matching | 10 | Hard | [notes](dynamic-programming/lcs-strings/regex-matching.md) |

### LIS
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Longest Increasing Subsequence | 300 | Medium | [notes](dynamic-programming/lis/longest-increasing-subsequence.md) |
| 2 | Russian Doll Envelopes | 354 | Hard | [notes](dynamic-programming/lis/russian-doll-envelopes.md) |
| 3 | Number of LIS | 673 | Medium | [notes](dynamic-programming/lis/number-of-lis.md) |
| 4 | Increasing Triplet Subsequence | 334 | Medium | [notes](dynamic-programming/lis/increasing-triplet.md) |

### Interval DP
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Burst Balloons | 312 | Hard | [notes](dynamic-programming/intervals/burst-balloons.md) |
| 2 | Strange Printer | 664 | Hard | [notes](dynamic-programming/intervals/strange-printer.md) |
| 3 | Minimum Cost to Cut a Stick | 1547 | Hard | [notes](dynamic-programming/intervals/min-cost-cut-stick.md) |
| 4 | Palindrome Partitioning II | 132 | Hard | [notes](dynamic-programming/intervals/palindrome-partitioning-ii.md) |

### State Machine DP
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Best Time to Buy/Sell Stock III | 123 | Hard | [notes](dynamic-programming/state-machine/stock-iii.md) |
| 2 | Best Time to Buy/Sell Stock IV | 188 | Hard | [notes](dynamic-programming/state-machine/stock-iv.md) |
| 3 | Best Time to Buy/Sell with Cooldown | 309 | Medium | [notes](dynamic-programming/state-machine/stock-cooldown.md) |
| 4 | Best Time to Buy/Sell with Fee | 714 | Medium | [notes](dynamic-programming/state-machine/stock-fee.md) |

---

## Bit Manipulation
| # | Problem | LC | Difficulty | Notes |
|---|---|---|---|---|
| 1 | Single Number | 136 | Easy | [notes](bit-manipulation/single-number.md) |
| 2 | Single Number II | 137 | Medium | [notes](bit-manipulation/single-number-ii.md) |
| 3 | Missing Number | 268 | Easy | [notes](bit-manipulation/missing-number.md) |
| 4 | Reverse Bits | 190 | Easy | [notes](bit-manipulation/reverse-bits.md) |
| 5 | Number of 1 Bits | 191 | Easy | [notes](bit-manipulation/number-of-1-bits.md) |
| 6 | Counting Bits | 338 | Easy | [notes](bit-manipulation/counting-bits.md) |
| 7 | Sum of Two Integers | 371 | Medium | [notes](bit-manipulation/sum-two-integers.md) |
| 8 | Power of Two | 231 | Easy | [notes](bit-manipulation/power-of-two.md) |
| 9 | Pow(x, n) | 50 | Medium | [notes](bit-manipulation/pow-x-n.md) |

---

## Note Template

Each problem note follows this structure:

```
# Problem Name — LC #

**Pattern:**
**Difficulty:**
**Companies:**

---

## Problem
## Intuition
## Algorithm
## Code — Java
## Complexity
## Dry Run
## Edge Cases
## Common Mistakes
## Related Problems
```
