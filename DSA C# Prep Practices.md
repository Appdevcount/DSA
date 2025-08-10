# Consolidated DSA Learning Track — **C#**

*(12‑week plan, explanations, Big‑O measurement, code snippets, and a 75‑problem appendix with approach & complexities)*

Nice — below is a single, consolidated guide you can save as a `README.md`. I kept everything focused on **C#**, followed your weekly structure, added explanations, Big‑O measurement tips (including an empirical Stopwatch snippet), and an appendix of **75 practice problems** grouped by topic with short explanations, the solution approach, and time/space complexity.
If you want, I can convert this to a downloadable `.md` or a printable PDF next.

---

# Table of Contents

1. Overview & Goals
2. 12‑week Study Plan (mapped to your Week 1–12)
3. How to use this track (daily routine, practice cadence, Do’s & Don’ts)
4. Big‑O: formal definition, how to measure, rules, and C# examples
5. Core data structures & C# implementations (short, practical)
6. Core algorithms & patterns with C# examples (sorting, search, graph, DP, backtracking)
7. Problem‑solving patterns (two pointers, sliding window, prefix sums, fast/slow, greedy)
8. Empirical complexity measurement in C# (Stopwatch)
9. Interview & practice tips (mock interviews, how to present solution)
10. Appendix — **LeetCode‑style 75 problems** grouped by topic with explanation, approach, and complexity

---

# 1) Overview & Goals

* Audience: .NET / C# developer preparing for interviews and strong algorithmic foundations.
* Outcome after 12 weeks: comfortable with arrays/strings/linked lists/stacks/queues/trees/graphs/heap/tries/DP/backtracking + able to solve medium→hard interview problems and reason about Big‑O.

---

# 2) 12‑Week Study Plan (mapped from your structure)

## Week 1–4: Beginner (Fundamentals & Basics)

**Goals:** arrays, strings, linked lists (singly/doubly), stacks, queues, sorting basics, searching, recursion, Big‑O.
**Daily plan sample**

* Day 1–2: Theory + implement arrays & string utilities (reverse, palindrome, frequency).
* Day 3: Linked lists (create, reverse, insert, delete).
* Day 4: Implement stack & queue (and use .NET `Stack<T>`/`Queue<T>`).
* Day 5: Sorting: Bubble, Selection, Insertion — implement and analyze.
* Day 6: Searching: Linear & Binary Search (write iterative & recursive).
* Day 7: 3–5 easy problems (LeetCode/HackerRank) from these topics.

## Week 5–8: Intermediate

**Goals:** trees, BSTs, heaps, priority queues, graphs, hash tables, efficient sorting (merge/quick/heap), DFS/BFS, intro DP.
**Weekly plan**

* Day 1–2: Binary trees, BST operations, traversals (in/ pre / post / level).
* Day 3: Heaps & PriorityQueue usage and custom implementation.
* Day 4: Graphs: adjacency list, DFS, BFS.
* Day 5: Merge Sort, Quick Sort, Heap Sort implementations & analysis.
* Day 6: Intro DP (memoization + bottom‑up examples: Fibonacci, knapsack).
* Day 7: 4–6 medium problems & timed challenges.

## Week 9–12: Professional

**Goals:** advanced graphs, advanced DP, segment trees / Fenwick, tries, bit manipulation; emphasis on hard problems, mocks.
**Weekly plan**

* Day 1–2: Graph algorithms (Dijkstra, Bellman‑Ford, topological sort, SCCs).
* Day 3: Advanced DP (LIS, DP on trees, DP with bitmasking).
* Day 4: Segment trees / Fenwick (range queries & updates).
* Day 5: Tries, bit manipulation, advanced trees.
* Day 6: Solve hard problems + mock interviews.
* Day 7: Review & focus weak spots.

---

# 3) How to use this track (practical)

* *One topic at a time.* Implement from scratch, then compare to library versions.
* Practice: 4–6 problems / week (beginner weeks lower, intermediate more). Mix of easy/medium/hard.
* Timeboxing: 60–90 minutes per practice session; for hard problems do 2 sessions.
* Keep a “mistake log” — store problem id, core idea, variant ideas, and follow‑ups.

---

# 4) Big‑O: definition, rules, and C# examples

## What is Big‑O?

Big‑O notation describes *asymptotic upper bound* on time (or space) as a function of input size `n`. It's about growth — not exact time. Use worst‑case unless specified.

## Big‑O categories (summary)

* **O(1)** constant
* **O(log n)** logarithmic (binary search)
* **O(n)** linear
* **O(n log n)** typical sorting (merge/quick average)
* **O(n^2)** quadratic (nested loops)
* **O(2^n)** exponential (naïve recursion over subsets)
* **O(n!)** factorial (all permutations)

## Rules / Tips to compute Big‑O

* Drop constants: `3n + 2 -> O(n)`.
* Keep dominant term: `n^2 + n -> O(n^2)`.
* For nested loops multiply: outer m, inner n → O(m\*n).
* For sequential statements add, but asymptotically the largest term dominates.

---

## C# examples (short, with complexity)

### O(1): constant — array access

```csharp
int FirstElement(int[] arr) => arr[0]; // O(1) time, O(1) space
```

### O(n): linear — sum of array

```csharp
int Sum(int[] arr) {
    int s = 0;
    foreach (var x in arr) s += x;
    return s; // O(n) time, O(1) space
}
```

### O(log n): binary search

```csharp
int BinarySearch(int[] arr, int target) {
    int l = 0, r = arr.Length - 1;
    while (l <= r) {
        int m = l + (r - l) / 2;
        if (arr[m] == target) return m;
        if (arr[m] < target) l = m + 1; else r = m - 1;
    }
    return -1; // O(log n) time, O(1) space
}
```

### O(n log n): merge sort (time), O(n) space

```csharp
int[] MergeSort(int[] arr) {
    if (arr.Length <= 1) return arr;
    int mid = arr.Length / 2;
    var left = MergeSort(arr[..mid]);
    var right = MergeSort(arr[mid..]);
    return Merge(left, right);
}
// Merge is O(n) time; recurrence T(n)=2T(n/2)+O(n) => O(n log n)
```

### O(n^2): nested loops

```csharp
void PairPrint(int[] arr) {
    for (int i = 0; i < arr.Length; i++)
        for (int j = 0; j < arr.Length; j++)
            Console.WriteLine($"{arr[i]}, {arr[j]}");
} // O(n^2) time, O(1) extra space
```

### O(2^n): recursive Fibonacci (naïve)

```csharp
int Fib(int n) {
    if (n < 2) return n;
    return Fib(n-1) + Fib(n-2);
} // O(2^n) time, O(n) recursion stack
```

### O(n!): permutations

```csharp
void Permute(List<int> cur, List<int> nums, List<List<int>> res) {
    if (cur.Count == nums.Count) { res.Add(new List<int>(cur)); return; }
    for (int i=0;i<nums.Count;i++) {
        if (cur.Contains(nums[i])) continue;
        cur.Add(nums[i]);
        Permute(cur, nums, res);
        cur.RemoveAt(cur.Count-1);
    }
} // O(n!) time
```

---

# 5) Core Data Structures — brief C# implementations & notes

I’ll show compact, production‑like snippets you can paste into a console app / unit test.

### Singly Linked List (basic)

```csharp
class ListNode {
    public int Val;
    public ListNode Next;
    public ListNode(int v){ Val=v; }
}
class LinkedList {
    public ListNode Head;
    public void AddFirst(int v) {
        var node = new ListNode(v) { Next = Head };
        Head = node;
    }
    // Reverse in-place: O(n)
    public void Reverse() {
        ListNode prev = null, cur = Head;
        while (cur != null) { var nxt = cur.Next; cur.Next = prev; prev = cur; cur = nxt; }
        Head = prev;
    }
}
```

### Stack / Queue custom (but use `Stack<T>`/`Queue<T>` in interviews)

```csharp
class MyStack<T> {
    private List<T> _list = new();
    public void Push(T v) => _list.Add(v);
    public T Pop(){ var v=_list[^1]; _list.RemoveAt(_list.Count-1); return v; }
    public T Peek() => _list[^1];
}
```

### Binary Tree (Node + inorder traversal)

```csharp
class TreeNode { public int Val; public TreeNode Left, Right; public TreeNode(int v)=>Val=v; }
void Inorder(TreeNode root) {
    if (root == null) return;
    Inorder(root.Left);
    Console.WriteLine(root.Val);
    Inorder(root.Right);
}
```

### Binary Heap (min‑heap) — minimal

```csharp
class MinHeap {
    private List<int> heap = new();
    public void Push(int x) {
        heap.Add(x); int i = heap.Count - 1;
        while (i>0) { int p=(i-1)/2; if (heap[p]<=heap[i]) break; (heap[p],heap[i])=(heap[i],heap[p]); i=p; }
    }
    public int Pop() {
        int res = heap[0]; heap[0] = heap[^1]; heap.RemoveAt(heap.Count-1);
        int i=0;
        while (true) {
            int l=2*i+1, r=2*i+2, smallest=i;
            if (l<heap.Count && heap[l]<heap[smallest]) smallest=l;
            if (r<heap.Count && heap[r]<heap[smallest]) smallest=r;
            if (smallest==i) break;
            (heap[i],heap[smallest])=(heap[smallest],heap[i]); i=smallest;
        }
        return res;
    }
}
```

### Trie (prefix tree)

```csharp
class TrieNode {
    public TrieNode[] Kids = new TrieNode[26];
    public bool End;
}
class Trie {
    private TrieNode root = new();
    public void Insert(string w) {
        var cur = root;
        foreach(var ch in w) {
            int i = ch - 'a';
            if (cur.Kids[i] == null) cur.Kids[i] = new TrieNode();
            cur = cur.Kids[i];
        }
        cur.End = true;
    }
    public bool Search(string w) {
        var cur = root;
        foreach(var ch in w) { cur = cur.Kids[ch - 'a']; if (cur==null) return false; }
        return cur.End;
    }
}
```

### Union‑Find (Disjoint Set)

```csharp
class DSU {
    int[] p, r;
    public DSU(int n) { p = Enumerable.Range(0,n).ToArray(); r = new int[n]; }
    public int Find(int a) => p[a] == a ? a : (p[a] = Find(p[a]));
    public bool Union(int a, int b) {
        a = Find(a); b = Find(b); if (a==b) return false;
        if (r[a] < r[b]) (a,b)=(b,a);
        p[b]=a; if (r[a]==r[b]) r[a]++; return true;
    }
}
```

### Graph (adjacency list + BFS)

```csharp
void BFS(List<int>[] graph, int start) {
    var q = new Queue<int>(); var seen = new bool[graph.Length];
    q.Enqueue(start); seen[start]=true;
    while (q.Count>0) {
        int u = q.Dequeue();
        foreach(var v in graph[u]) if (!seen[v]) { seen[v]=true; q.Enqueue(v); }
    }
}
```

---

# 6) Core Algorithms & patterns (C# sketches)

### Merge Sort (C#)

```csharp
int[] MergeSort(int[] a) {
    if (a.Length<=1) return a;
    int m = a.Length/2;
    var L = MergeSort(a[..m]); var R = MergeSort(a[m..]);
    return Merge(L,R);
}
```

### Quick Sort (inplace)

```csharp
void QuickSort(int[] a, int l, int r) {
    if (l>=r) return;
    int pivot = a[(l+r)/2], i=l, j=r;
    while (i<=j) {
        while (a[i]<pivot) i++;
        while (a[j]>pivot) j--;
        if (i<=j) { (a[i],a[j])=(a[j],a[i]); i++; j--; }
    }
    QuickSort(a,l,j); QuickSort(a,i,r);
}
```

### Dijkstra (using `PriorityQueue<TElement,TPriority>` .NET 6+)

```csharp
int[] Dijkstra(List<(int to,int w)>[] g, int src) {
    int n = g.Length; var dist = Enumerable.Repeat(int.MaxValue,n).ToArray();
    var pq = new PriorityQueue<int,int>();
    dist[src] = 0; pq.Enqueue(src,0);
    while (pq.Count>0) {
        pq.TryDequeue(out var u, out var du);
        if (du > dist[u]) continue;
        foreach (var (v,w) in g[u]) {
            if (dist[v] > dist[u] + w) {
                dist[v] = dist[u] + w;
                pq.Enqueue(v, dist[v]);
            }
        }
    }
    return dist;
}
```

### DP (memoization example — Fibonacci)

```csharp
int FibMemo(int n, int[] memo) {
    if (n<2) return n;
    if (memo[n]!=-1) return memo[n];
    return memo[n] = FibMemo(n-1,memo) + FibMemo(n-2,memo);
}
```

### Backtracking (Permutations)

```csharp
void Permute(int[] nums, List<int> cur, List<IList<int>> res, bool[] used) {
    if (cur.Count == nums.Length) { res.Add(new List<int>(cur)); return; }
    for (int i=0;i<nums.Length;i++) {
        if (used[i]) continue;
        used[i] = true; cur.Add(nums[i]);
        Permute(nums, cur, res, used);
        used[i] = false; cur.RemoveAt(cur.Count-1);
    }
}
```

---

# 7) Problem‑solving patterns (with tiny C# examples)

### Two pointers — Sorted array two-sum (returns indices)

```csharp
(int,int) TwoSumSorted(int[] a, int target) {
    int l=0, r=a.Length-1;
    while (l<r) {
        int s = a[l] + a[r];
        if (s==target) return (l,r);
        if (s<target) l++; else r--;
    }
    return (-1,-1);
}
```

### Sliding window — longest substring w/out repeat

```csharp
int LongestUnique(string s) {
    var last = new int[128];
    Array.Fill(last, -1);
    int res=0, l=0;
    for (int r=0;r<s.Length;r++) {
        l = Math.Max(l, last[s[r]]+1);
        res = Math.Max(res, r-l+1);
        last[s[r]] = r;
    }
    return res;
}
```

### Fast & slow pointers — detect cycle in linked list

```csharp
bool HasCycle(ListNode head) {
    var slow=head; var fast=head;
    while (fast!=null && fast.Next!=null) {
        slow = slow.Next; fast = fast.Next.Next;
        if (slow==fast) return true;
    }
    return false;
}
```

---

# 8) Empirical measurement in C# (Stopwatch)

When you want to *measure* runtime (for experiments), use `System.Diagnostics.Stopwatch`. Remember: always run enough iterations and consider JIT warmup.

```csharp
using System.Diagnostics;
void Measure(Action action, int runs=10) {
    var sw = new Stopwatch();
    // warmup
    action();
    long total = 0;
    for (int i=0;i<runs;i++) {
        sw.Restart();
        action();
        sw.Stop();
        total += sw.ElapsedTicks;
    }
    Console.WriteLine($"Avg ticks: {total / runs}");
}
```

⚠️ Use this to compare algorithms empirically (not as a replacement for Big‑O reasoning). Use sufficiently large `n`, and avoid microbenchmarks noise.

---

# 9) Interview & practice tips

* Verbalize assumptions; state input size expectations and complexities.
* Always give worst/average/best if relevant.
* Start with a simple brute force solution, then optimize. Explain tradeoffs.
* Test on edge cases out loud: empty, single element, duplicates, etc.
* Keep code readable: clear variable names, small helper methods.
* Write tests or at least a few sample runs.

---

# 10) Appendix — **75 Practice Problems** (grouped by topic)

For each problem: **Title • Short prompt • Approach • Time / Space complexity • (compact reasoning / solution outline in C# where short)**

> I list 75 problems across the topics in your plan. These are classic interview problems (LeetCode-style). For each I give a succinct approach & complexity. If you want full, runnable C# solutions for any subset (e.g., top 20), I’ll provide them in a follow-up file.

---

## Arrays & Strings (15)

1. **Two Sum**

   * Prompt: Given array `nums` and `target`, return indices of two numbers that add to target.
   * Approach: Hash map value→index (one pass).
   * Complexity: O(n) time, O(n) space.
   * Reason: Store seen values; check complement.

2. **Best Time to Buy and Sell Stock (I)**

   * Prompt: Max single profit from one buy & sell.
   * Approach: Track min price so far, update max profit.
   * Complexity: O(n), O(1).

3. **Contains Duplicate**

   * Prompt: Any duplicate in array?
   * Approach: HashSet.
   * Complexity: O(n), O(n).

4. **Product of Array Except Self**

   * Prompt: Return array where each element is product of all others without division.
   * Approach: Prefix & suffix products (two passes).
   * Complexity: O(n), O(1) extra (output array allowed).

5. **Maximum Subarray (Kadane)**

   * Prompt: Max subarray sum.
   * Approach: Kadane's algorithm (running max).
   * Complexity: O(n), O(1).

6. **Move Zeroes**

   * Prompt: Move zeros to end preserving relative order.
   * Approach: Two pointers / write index.
   * Complexity: O(n), O(1).

7. **Rotate Array**

   * Prompt: Rotate array right by k.
   * Approach: Reverse whole, reverse first k, reverse rest.
   * Complexity: O(n), O(1).

8. **Reverse String**

   * Prompt: Reverse in place.
   * Approach: Two pointers.
   * Complexity: O(n), O(1).

9. **Valid Anagram**

   * Prompt: Check if two strings are anagrams.
   * Approach: Count frequency (array\[26] or dictionary).
   * Complexity: O(n), O(1) (26) or O(k).

10. **Longest Substring Without Repeating Characters**

    * Prompt: Longest unique-substring length.
    * Approach: Sliding window with last index map.
    * Complexity: O(n), O(min(n, charset)).

11. **Longest Palindromic Substring**

    * Prompt: Find longest palindromic substring.
    * Approach: Expand around center (O(n^2)) or Manacher (O(n)).
    * Complexity: O(n^2) naive, O(n) Manacher.

12. **Container With Most Water**

    * Prompt: Container with max area of two lines.
    * Approach: Two pointers shrinking toward center, updating max area.
    * Complexity: O(n), O(1).

13. **3Sum**

    * Prompt: Find unique triplets that sum to 0.
    * Approach: Sort + two pointers per index.
    * Complexity: O(n^2), O(1) extra.

14. **Merge Intervals**

    * Prompt: Merge overlapping intervals.
    * Approach: Sort by start, merge sequentially.
    * Complexity: O(n log n), O(n).

15. **Insert Interval**

    * Prompt: Insert and merge new interval.
    * Approach: Walk intervals, merge overlapping.
    * Complexity: O(n), O(n).

---

## Linked Lists (6)

16. **Reverse Linked List**

    * Prompt: Reverse singly linked list in place.
    * Approach: Iterative with prev/cur.
    * Complexity: O(n), O(1).

17. **Merge Two Sorted Lists**

    * Prompt: Merge two sorted singly lists into one.
    * Approach: Dummy head, pointer merge.
    * Complexity: O(n+m), O(1).

18. **Linked List Cycle**

    * Prompt: Detect cycle.
    * Approach: Fast & slow pointers (Floyd).
    * Complexity: O(n), O(1).

19. **Remove Nth Node From End**

    * Prompt: Remove Nth node from end in one pass.
    * Approach: Two pointers with gap n.
    * Complexity: O(n), O(1).

20. **Add Two Numbers (linked lists)**

    * Prompt: Sum two numbers represented by linked lists.
    * Approach: Add digit by digit with carry.
    * Complexity: O(max(m,n)), O(1) extra.

21. **Copy List with Random Pointer**

    * Prompt: Deep copy list with random pointers.
    * Approach: Interweave nodes approach O(n), O(1) extra (or hashmap O(n)).
    * Complexity: O(n), O(1) extra (interleaving method).

---

## Stacks & Queues (4)

22. **Valid Parentheses**

    * Approach: Stack, push open, pop & match closing. O(n), O(n).

23. **Min Stack**

    * Approach: Maintain auxiliary stack of mins or store pairs. O(1) per op amortized.

24. **Evaluate Reverse Polish Notation**

    * Approach: Stack for operands, apply operators. O(n), O(n).

25. **Sliding Window Maximum**

    * Approach: Deque maintains potential maximums (monotonic queue). O(n), O(n).

---

## Trees & BST (10)

26. **Binary Tree Inorder Traversal**

    * Approach: Recursion or iterative using stack. O(n), O(h) stack.

27. **Validate BST**

    * Approach: Inorder traversal should be strictly increasing. O(n), O(h).

28. **Maximum Depth of Binary Tree**

    * Approach: DFS recursion. O(n), O(h).

29. **Symmetric Tree**

    * Approach: Mirror check with BFS/DFS. O(n), O(h).

30. **Level Order Traversal**

    * Approach: BFS with queue. O(n), O(n).

31. **Lowest Common Ancestor of BST**

    * Approach: Use BST property to go left/right. O(h), O(1).

32. **Serialize and Deserialize Binary Tree**

    * Approach: Preorder with null markers, BFS with queue. O(n), O(n).

33. **Binary Tree Zigzag Level Order**

    * Approach: BFS with flipping order or use deque. O(n), O(n).

34. **Construct Binary Tree from Preorder and Inorder**

    * Approach: Recursively split by root index using a map for inorder positions. O(n), O(n).

35. **Convert Sorted Array to BST**

    * Approach: Middle element as root recursively. O(n), O(log n) recursion stack (balanced).

---

## Heaps / Sorting / Searching (6)

36. **Merge k Sorted Lists**

    * Approach: Min‑heap over heads. O(N log k) where N total nodes. Space O(k).

37. **Top K Frequent Elements**

    * Approach: Frequency map + heap (or bucket sort). O(n log k) or O(n).

38. **Kth Largest Element in an Array**

    * Approach: Quickselect (average O(n)), or heap O(n log k). Space O(1) or O(k).

39. **Sort Colors (Dutch National Flag)**

    * Approach: Three pointers / counting. O(n), O(1).

40. **Search in Rotated Sorted Array**

    * Approach: Modified binary search deciding which half is sorted. O(log n).

41. **Find First and Last Position of Element in Sorted Array**

    * Approach: Two binary searches for leftmost & rightmost. O(log n).

---

## Graphs (8)

42. **Number of Islands**

    * Prompt: Count connected components (grid).
    * Approach: DFS/BFS flood fill. O(m*n), O(m*n) recursion.

43. **Clone Graph**

    * Approach: BFS/DFS + hashmap to copy nodes. O(V+E), O(V).

44. **Course Schedule (detect cycle in directed graph)**

    * Approach: DFS coloring or Kahn's topo sort. O(V+E), O(V).

45. **Course Schedule II (topo order)**

    * Approach: Kahn's algorithm or DFS postorder. O(V+E).

46. **Word Ladder (shortest path transform)**

    * Approach: BFS on word graph (or bidirectional BFS). O(N \* L^2) approx.

47. **Network Delay Time (single source Dijkstra)**

    * Approach: Dijkstra with priority queue. O(E log V).

48. **Graph Valid Tree**

    * Approach: Check edges == n-1 and connectivity via DFS/UnionFind. O(n).

49. **Minimum Height Trees**

    * Approach: Trim leaves BFS approach. O(n).

---

## Dynamic Programming (10)

50. **Climbing Stairs**

    * Approach: Fibonacci DP. O(n), O(1) or O(n).

51. **Coin Change**

    * Approach: DP unbounded knapsack (bottom-up). O(amount \* ncoins).

52. **Longest Increasing Subsequence (LIS)**

    * Approach: DP O(n^2) or patience sorting / binary search O(n log n). Space O(n).

53. **Maximum Product Subarray**

    * Approach: Track max and min (because of negatives). O(n).

54. **House Robber**

    * Approach: DP with two states. O(n), O(1).

55. **House Robber II (circular)**

    * Approach: Run two linear cases (exclude first or last). O(n).

56. **Decode Ways**

    * Approach: DP based on valid single or double digits. O(n).

57. **Unique Paths**

    * Approach: DP combinatorics / grid DP. O(n\*m).

58. **Word Break**

    * Approach: DP over prefixes (dictionary substrings). O(n^2) approx.

59. **Longest Palindromic Subsequence**

    * Approach: DP over substrings or LCS with reverse string. O(n^2).

---

## Backtracking (5)

60. **Permutations**

    * Approach: Backtracking with used\[]; O(n\*n!) time.

61. **Subsets**

    * Approach: Backtracking or bitmask iteration. O(n\*2^n).

62. **Combination Sum**

    * Approach: Backtracking choose/unchoose with sorted candidates. Complexity depends on branching.

63. **N‑Queens**

    * Approach: Backtracking with column/diag sets. O(n!) worst-case.

64. **Restore IP Addresses**

    * Approach: Backtracking with length constraints. Practical pruning.

---

## Bit Manipulation & Math (3)

65. **Single Number**

    * Approach: XOR all elements; pair cancel out. O(n), O(1).

66. **Number of 1 Bits**

    * Approach: n & (n-1) trick or built-in. O(#ones) or O(1) for fixed-size ints.

67. **Pow(x, n)**

    * Approach: Fast exponentiation (binary exponentiation). O(log n).

---

## Union‑Find / Advanced (3)

68. **Redundant Connection**

    * Approach: DSU: the first union that finds both nodes already connected is redundant. O(alpha(n)) per op.

69. **Number of Connected Components in Undirected Graph**

    * Approach: DSU or DFS. O(n + e).

70. **Accounts Merge**

    * Approach: DSU on emails or graph components. O(total emails \* α).

---

## Tries / Segment Tree / Fenwick (3)

71. **Implement Trie (Insert/Search/StartsWith)**

    * Approach: Trie node array / dictionary. O(length) per op.

72. **Word Search II**

    * Approach: Trie + DFS backtracking to find many words with pruning. Complexity depends on board & words.

73. **Range Sum Query - Mutable (Segment Tree / Fenwick)**

    * Approach: Segment tree or Fenwick (BIT) for updates & range queries. Segment tree O(log n) update/query.

---

## Misc (2)

74. **LRU Cache**

    * Approach: Doubly linked list + Dictionary for O(1) get/put. O(1) per op.

75. **Design Twitter (or limited social feed)**

    * Approach: HashMap of user→tweets + min‑heap to merge followers' recent tweets. Complexity depends on feed length and k.

---

# How to use the appendix

* Treat problems in each block progressively: start with arrays & strings, then lists, stacks/queues, trees, etc.
* For each problem: first write a brute force and analyze; then optimize to the expected complexity.
* Track problems you couldn't solve; revisit after 2–3 days.

---

# A compact example — **Two Sum** (full C#)

```csharp
public int[] TwoSum(int[] nums, int target) {
    var map = new Dictionary<int,int>();
    for (int i=0;i<nums.Length;i++){
        int need = target - nums[i];
        if (map.TryGetValue(need, out int idx)) return new[]{idx, i};
        if (!map.ContainsKey(nums[i])) map[nums[i]] = i;
    }
    return Array.Empty<int>();
} // O(n) time, O(n) space
```

---

# Final tips & next steps

* Keep code minimal and well‑documented. Prefer readability in interviews.
* Practice whiteboard-style explanation: talk about approach, complexity, edge cases, then code.
* Use company/role‑specific questions near interview time.
* If you'd like, I can:

  * Export this to a `.md` file and attach it; or
  * Produce full, runnable C# solutions for the **top 20** problems from the appendix (with unit tests); or
  * Create a spaced schedule (daily checklist) you can mark completed.

Which of those would you like next?


Alright — I’ll make you a **full “LeetCode C# DSA Master Template”** in Markdown format so you can copy-paste and adapt instantly for any problem type.

This will cover:

* **General boilerplate & speed hacks**
* **Patterns for every major DSA category** (arrays, strings, linked lists, trees, graphs, heaps, backtracking, DP, union-find, bit manipulation, etc.)
* **Problem-specific mini-templates**
* **C# nuances & pitfalls**

I’ll structure it so you can scroll and jump to exactly what you need.

---

# **LeetCode C# DSA Master Template**

*(All code in C# 10 / .NET 6+, ready for LeetCode)*

---

## **0. General Boilerplate**

```csharp
// Namespace & using statements
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

public class Solution
{
    // Place your methods here
}
```

**Tips**

* Use `var` for brevity.
* Use `Array.Empty<T>()` instead of `new T[0]`.
* Use `StringBuilder` for building strings in loops.

---

## **1. Arrays & Two Pointers**

**Two Sum Sorted**

```csharp
public int[] TwoSumSorted(int[] nums, int target)
{
    int left = 0, right = nums.Length - 1;
    while (left < right)
    {
        int sum = nums[left] + nums[right];
        if (sum == target) return new[] { left, right };
        if (sum < target) left++;
        else right--;
    }
    return Array.Empty<int>();
}
```

**Sliding Window Max Sum**

```csharp
public int MaxSumSubarray(int[] nums, int k)
{
    int sum = 0, maxSum = int.MinValue;
    for (int i = 0; i < nums.Length; i++)
    {
        sum += nums[i];
        if (i >= k - 1)
        {
            maxSum = Math.Max(maxSum, sum);
            sum -= nums[i - k + 1];
        }
    }
    return maxSum;
}
```

---

## **2. Strings**

**Reverse String**

```csharp
public void ReverseString(char[] s)
{
    int left = 0, right = s.Length - 1;
    while (left < right)
    {
        (s[left], s[right]) = (s[right], s[left]);
        left++;
        right--;
    }
}
```

**Anagram Check**

```csharp
public bool IsAnagram(string s, string t)
{
    if (s.Length != t.Length) return false;
    var count = new int[26];
    foreach (var c in s) count[c - 'a']++;
    foreach (var c in t) if (--count[c - 'a'] < 0) return false;
    return true;
}
```

---

## **3. Linked List**

**Reverse Linked List**

```csharp
public ListNode ReverseList(ListNode head)
{
    ListNode prev = null;
    while (head != null)
    {
        var next = head.next;
        head.next = prev;
        prev = head;
        head = next;
    }
    return prev;
}
```

---

## **4. Trees**

**DFS Recursive**

```csharp
public void DFS(TreeNode node)
{
    if (node == null) return;
    DFS(node.left);
    DFS(node.right);
}
```

**BFS Level Order**

```csharp
public IList<IList<int>> LevelOrder(TreeNode root)
{
    var result = new List<IList<int>>();
    if (root == null) return result;

    var queue = new Queue<TreeNode>();
    queue.Enqueue(root);

    while (queue.Count > 0)
    {
        var size = queue.Count;
        var level = new List<int>();
        for (int i = 0; i < size; i++)
        {
            var node = queue.Dequeue();
            level.Add(node.val);
            if (node.left != null) queue.Enqueue(node.left);
            if (node.right != null) queue.Enqueue(node.right);
        }
        result.Add(level);
    }
    return result;
}
```

---

## **5. Graphs**

**BFS**

```csharp
public void BFS(Dictionary<int, List<int>> graph, int start)
{
    var visited = new HashSet<int>();
    var queue = new Queue<int>();
    queue.Enqueue(start);
    visited.Add(start);

    while (queue.Count > 0)
    {
        var node = queue.Dequeue();
        foreach (var nei in graph[node])
        {
            if (visited.Add(nei)) queue.Enqueue(nei);
        }
    }
}
```

**DFS**

```csharp
public void DFS(Dictionary<int, List<int>> graph, int node, HashSet<int> visited)
{
    if (!visited.Add(node)) return;
    foreach (var nei in graph[node]) DFS(graph, nei, visited);
}
```

---

## **6. Heaps**

**Priority Queue (Min-Heap)**

```csharp
var pq = new PriorityQueue<int, int>();
pq.Enqueue(5, 5);
pq.Enqueue(1, 1);
int min = pq.Dequeue();
```

---

## **7. Backtracking**

**Permutations**

```csharp
public IList<IList<int>> Permute(int[] nums)
{
    var result = new List<IList<int>>();
    void Backtrack(List<int> path, bool[] used)
    {
        if (path.Count == nums.Length)
        {
            result.Add(new List<int>(path));
            return;
        }
        for (int i = 0; i < nums.Length; i++)
        {
            if (used[i]) continue;
            used[i] = true;
            path.Add(nums[i]);
            Backtrack(path, used);
            path.RemoveAt(path.Count - 1);
            used[i] = false;
        }
    }
    Backtrack(new List<int>(), new bool[nums.Length]);
    return result;
}
```

---

## **8. Dynamic Programming**

**Fibonacci**

```csharp
public int Fib(int n)
{
    if (n < 2) return n;
    int a = 0, b = 1;
    for (int i = 2; i <= n; i++)
    {
        int temp = a + b;
        a = b;
        b = temp;
    }
    return b;
}
```

**0/1 Knapsack**

```csharp
public int Knapsack(int[] weights, int[] values, int W)
{
    var dp = new int[weights.Length + 1, W + 1];
    for (int i = 1; i <= weights.Length; i++)
    {
        for (int w = 0; w <= W; w++)
        {
            dp[i, w] = dp[i - 1, w];
            if (weights[i - 1] <= w)
                dp[i, w] = Math.Max(dp[i, w], values[i - 1] + dp[i - 1, w - weights[i - 1]]);
        }
    }
    return dp[weights.Length, W];
}
```

---

## **9. Union-Find (Disjoint Set)**

```csharp
public class UnionFind
{
    int[] parent, rank;
    public UnionFind(int n)
    {
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) parent[i] = i;
    }

    public int Find(int x)
    {
        if (parent[x] != x) parent[x] = Find(parent[x]);
        return parent[x];
    }

    public void Union(int x, int y)
    {
        int rootX = Find(x), rootY = Find(y);
        if (rootX == rootY) return;
        if (rank[rootX] < rank[rootY]) parent[rootX] = rootY;
        else if (rank[rootX] > rank[rootY]) parent[rootY] = rootX;
        else { parent[rootY] = rootX; rank[rootX]++; }
    }
}
```

---

## **10. Bit Manipulation**

```csharp
public int SingleNumber(int[] nums)
{
    int res = 0;
    foreach (var num in nums) res ^= num;
    return res;
}
```

---

I can now save this as a **ready-to-download `.md` file** so you can keep it as your **personal C# DSA LeetCode cheatsheet** with clickable sections.

Do you want me to generate that `.md` file now so you can store it and use it offline?


Got it — you’re asking for more than just syntax templates.
You want **C#-specific thinking patterns, tips, and “mental shortcuts”** for all kinds of DSA problems so that when you’re solving LeetCode in C#, you’re already aware of:

* What **C# language features** make certain DSA problems easier
* Common **optimizations** and pitfalls in .NET
* How to **translate DSA logic into idiomatic C#** instead of just copying Java/Python style
* How to pick the right data structures from `System.Collections` and `System.Linq`

Here’s what I’d suggest as a **full guide**.

---

# **C# Tips & Tricks for All DSA Possibilities**

---

## **1. General Speed & Memory Tips**

* **Use arrays over lists** when the size is fixed — faster indexing.
* **Prefer `Span<T>` or `ReadOnlySpan<T>`** for subarray processing without allocation.
* Avoid `ToList()` / `ToArray()` unless necessary — each call allocates memory.
* Use **`StringBuilder` for concatenation** in loops — `+` for strings in loops is O(n²).
* **Minimize boxing/unboxing** by using generics with value types (avoid `object` collections).
* `var` can make code cleaner but don’t sacrifice clarity in interviews.

---

## **2. Arrays & Lists**

* **Initialization**:

  ```csharp
  var arr = new int[5]; // default zeros
  var list = new List<int> {1, 2, 3};
  ```
* **Sorting with custom comparer**:

  ```csharp
  Array.Sort(arr, (a, b) => a.CompareTo(b)); // ascending
  ```
* **Prefix sums**: Use `int[] prefix = new int[n+1];` for O(1) range sums.

---

## **3. Strings**

* Strings are **immutable** — always consider `StringBuilder` for heavy modifications.
* For frequency count:

  ```csharp
  var count = new int[26];
  foreach (var c in s) count[c - 'a']++;
  ```
* `s.AsSpan(start, length)` lets you handle substrings without new allocations.
* **`string.Equals(a, b, StringComparison.Ordinal)`** is faster than default equality.

---

## **4. Dictionaries & HashSets**

* **Dictionaries**: Best for O(1) lookup; avoid repeated `.ContainsKey()` + index — use `TryGetValue()`.
* **HashSet**: Use for uniqueness; avoids duplicates automatically.
* **Initialization with capacity** avoids rehashing:

  ```csharp
  var dict = new Dictionary<int, int>(n);
  ```

---

## **5. Linked Lists**

* LeetCode uses:

  ```csharp
  public class ListNode {
      public int val;
      public ListNode next;
      public ListNode(int val=0, ListNode next=null) { this.val = val; this.next = next; }
  }
  ```
* Use **fast/slow pointers** for cycle detection.
* Always keep track of a **dummy head** for easier insert/delete logic.

---

## **6. Stacks & Queues**

* Stack:

  ```csharp
  var stack = new Stack<int>();
  stack.Push(1); stack.Pop();
  ```
* Queue:

  ```csharp
  var q = new Queue<int>();
  q.Enqueue(1); q.Dequeue();
  ```
* **Deque simulation**: `LinkedList<T>` can push/pop from both ends.

---

## **7. Trees**

* BFS → use `Queue<TreeNode>`
* DFS → recursion or explicit `Stack<TreeNode>`
* Null-check early:

  ```csharp
  if (root == null) return;
  ```
* Leverage **tuples** for passing multiple return values:

  ```csharp
  (int height, bool balanced) DFS(TreeNode node) { ... }
  ```

---

## **8. Graphs**

* Represent as:

  ```csharp
  var graph = new Dictionary<int, List<int>>();
  ```
* BFS → `Queue<int>`, visited set
* DFS → recursion (watch out for stack overflow in huge graphs; convert to iterative if needed)
* Topological sort → `Queue<int>` with in-degree count

---

## **9. Heaps**

* Use `.NET 6+` `PriorityQueue<TElement, TPriority>`:

  ```csharp
  var pq = new PriorityQueue<int, int>();
  pq.Enqueue(5, 5);
  var min = pq.Dequeue();
  ```
* For max-heap, use negative priorities:

  ```csharp
  pq.Enqueue(5, -5);
  ```

---

## **10. Backtracking**

* Always track:

  * **Path list** (current solution)
  * **Visited set / bool\[]** (to avoid repetition)
* Use **`yield return`** for generating solutions lazily.
* Avoid excessive list copying — modify and revert.

---

## **11. Dynamic Programming**

* 1D optimization: If `dp[i]` only depends on `dp[i-1]`, use rolling array.
* Dictionary for sparse states:

  ```csharp
  var dp = new Dictionary<(int, int), int>();
  ```
* Initialize with `Array.Fill()` for default values.

---

## **12. Union-Find**

* Always compress paths:

  ```csharp
  if (parent[x] != x) parent[x] = Find(parent[x]);
  ```
* Use rank/size for balancing.

---

## **13. Bit Manipulation**

* **Check kth bit**: `(num & (1 << k)) != 0`
* **Set kth bit**: `num |= (1 << k)`
* **Clear kth bit**: `num &= ~(1 << k)`
* **Toggle kth bit**: `num ^= (1 << k)`

---

## **14. C#-Only Gotchas**

* LINQ is clean but **can be slower** in tight loops.
* Avoid `.OrderBy().ToList()` for simple sorts — use `Array.Sort()`.
* Value types (`struct`) are copied by value — avoid large structs in recursion.

---

If you want, I can now make a **massive Markdown “C# DSA Thinking Guide”** that combines this with **ready-to-use code templates** so you have **both strategy + code** in one place for every LeetCode category.

That would make it your **C# DSA brain + hands in one file**.
Do you want me to make that?


