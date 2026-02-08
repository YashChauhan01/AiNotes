# AI Search Strategies - Complete Notes

## Table of Contents
1. [Introduction to Search Strategies](#introduction)
2. [Evaluation Parameters](#evaluation-parameters)
3. [Uninformed Search vs Informed Search](#uninformed-vs-informed)
4. [Breadth-First Search (BFS)](#breadth-first-search)
5. [Depth-First Search (DFS)](#depth-first-search)
6. [Uniform Cost Search](#uniform-cost-search)
7. [Bidirectional Search](#bidirectional-search)
8. [Comparison Summary](#comparison-summary)

---

## Introduction to Search Strategies

### Why Search is Important?

**Key Importance:**
- One of the most important topics in entire Computer Science (not just AI)
- Converting any problem to a graph problem is relatively easy
- Always advisable to convert problem → Graph → Solve

**Definition:**
> "Search strategies refer to systematic methods and approaches used to explore and find relevant information and solutions within a given search space or dataset"

### Two Main Categories

```
Search Strategies
├── Uninformed Search (Blind Search)
└── Informed Search (Heuristic Search)
```

---

## Evaluation Parameters

### Four Key Parameters to Evaluate Search Algorithms

**1. Completeness**

**Definition:**
> "Determines if search technique guarantees finding a solution if one exists within the search space"

**Key Questions:**
- If solution exists, will algorithm definitely find it?
- Can algorithm get stuck without finding existing solution?

**Example:**
```
Search Space has solution: YES
Algorithm finds it: ???

Complete Algorithm → Guaranteed to find it
Incomplete Algorithm → Might miss it even if it exists
```

---

**2. Time Complexity**

**Definition:** How much time the algorithm takes to find solution

**Typical Notation:**
```
O(b^d)

Where:
b = Branching factor (how many children each node can have)
d = Depth (how deep we need to go to find solution)
```

---

**3. Space Complexity**

**Definition:** How much memory the algorithm requires

**Considerations:**
- Memory for storing nodes
- Queue/Stack requirements
- Visited nodes tracking

---

**4. Optimality**

**Definition:**
> "Determines whether the search technique can find the best or optimal solution among all possible solutions"

**Two Types of Problems:**
```
Decision Problems:
└── Answer: Yes or No

Optimization Problems:
└── Answer: Best solution among many
└── Example: Many paths from source to destination
            → Find shortest/optimal path
```

**Key Question:**
- Does algorithm guarantee the best possible solution?
- Or just any solution?

---

## Uninformed vs Informed Search

### Uninformed Search

**Also Known As:**
- Blind Search
- Brute Force Search
- Exhaustive Search

**Definition:**
> "Explores the search space without any specific information or heuristic about the problem"

**Characteristics:**
```
No Information:
├── No clues about goal location
├── No guidance toward solution
└── No domain knowledge

Approach:
├── Systematic exploration (predetermined order)
└── OR Random selection
```

**Example: Array Search Without Information**
```
Array: [5, 2, 8, 1, 9, 3, 7]
Find: 7

No information that array is sorted
→ Must check sequentially or randomly
→ This is Uninformed Search
```

---

### Advantages of Uninformed Search

```
✓ Very simple to design
✓ Easy to understand
✓ Easy to implement
✓ No need for domain knowledge
```

---

### Disadvantages of Uninformed Search

```
✗ Inefficient (time-consuming)
✗ May explore entire search space
✗ No optimization
✗ Exhaustive search required
```

**Why Inefficient?**
```
Without Information:
└── Must check everything exhaustively

With Information (sorted array):
└── Can use Binary Search (much faster)
```

---

### Informed Search

**Also Known As:**
- Heuristic Search

**Definition:**
> "Utilizes domain-specific information and heuristics to guide the search toward more promising areas"

**Characteristics:**
```
Has Information:
├── Clues about goal location
├── Knowledge about path cost
├── Distance estimates
└── Domain-specific insights
```

**Real-World Analogy: Police Search**
```
Uninformed Approach:
└── Search every house in entire city

Informed Approach:
└── Informant gives tip about specific area
└── Search only those 2-4 houses
└── This is Informed Search
```

---

### Knowledge Available in Informed Search

**Types of Information:**
```
1. How far from goal?
2. Path cost estimates
3. Direction toward goal
4. Heuristic functions
```

**Note:** Information doesn't have to be exact - can be estimates!

---

### Advantages of Informed Search

```
✓ More efficient
✓ Reduced search space
✓ Faster than uninformed search
✓ Uses intelligent guidance
```

**Example: Binary Search**
```
Information: Array is sorted

If value smaller:
└── Definitely in left half

If value larger:
└── Definitely in right half

Search space reduced by half each time
```

---

### Disadvantages of Informed Search

```
✗ Effectiveness depends on heuristic quality
✗ Bad heuristic → Wrong solution
✗ Inaccurate heuristic → Suboptimal solution
✗ Requires domain knowledge
```

**Critical Point:**
> "If your tip/heuristic is wrong, it can become a penalty instead of advantage"

---

### Comparison Table

| Aspect | Uninformed Search | Informed Search |
|--------|-------------------|-----------------|
| **Information** | No prior knowledge | Uses heuristics/domain knowledge |
| **Efficiency** | Less efficient | More efficient |
| **Search Space** | Explores exhaustively | Guided exploration |
| **Examples** | BFS, DFS, Uniform Cost | Best-First, A*, Hill Climbing |
| **Speed** | Slower | Faster (if heuristic good) |
| **Complexity** | Simpler | More complex |
| **Guarantee** | May guarantee completeness | Depends on heuristic accuracy |
| **Risk** | Slow but sure | Fast but depends on heuristic |

---

## Breadth-First Search (BFS)

### Definition

**What is BFS?**
> "An uninformed search strategy exploring all neighboring nodes at current level before moving to the next level, starting from the root"

**Level-by-Level Exploration:**
```
Level 0: Root node
    ↓
Level 1: All nodes at distance 1
    ↓
Level 2: All nodes at distance 2
    ↓
Level 3: All nodes at distance 3
    ...
```

---

### How BFS Works

**Approach:**
1. Start from root node
2. Visit all nodes at distance 1
3. Only then move to distance 2
4. Continue level by level

**Data Structure:** Queue (FIFO - First In First Out)

**Why Queue?**
- Sequential processing
- Maintains order
- FIFO perfect for level-by-level traversal

---

### BFS Example - Step by Step

**Given Graph:**
```
    A
   / \
  D   B
  |   |
  E   C
 /|\  |
F G  G
```

**Starting Node:** A

**Step-by-Step Execution:**

```
Step 1: Start
Queue: [A]
Visited: []

Step 2: Process A, add neighbors
Queue: [D, B]  (or [B, D] - order doesn't matter)
Visited: [A]

Step 3: Process D, add unvisited neighbors
D's neighbors: A (visited), E (new)
Queue: [B, E]
Visited: [A, D]

Step 4: Process B, add unvisited neighbors
B's neighbors: A (visited), C (new)
Queue: [E, C]
Visited: [A, D, B]

Step 5: Process E, add unvisited neighbors
E's neighbors: D (visited), C (already in queue), F (new), G (new)
Queue: [C, F, G]
Visited: [A, D, B, E]

Step 6: Process C
C's neighbors: B (visited), G (already in queue)
Queue: [F, G]
Visited: [A, D, B, E, C]

Step 7: Process F
Queue: [G]
Visited: [A, D, B, E, C, F]

Step 8: Process G
Queue: []
Visited: [A, D, B, E, C, F, G]
```

**Traversal Order:** A → D → B → E → C → F → G

---

### BFS Algorithm (Simplified)

```
Algorithm BFS(Graph, start):
1. Create empty Queue
2. Enqueue start node
3. Mark start as visited

4. While Queue is not empty:
   a. Dequeue front element (current)
   b. Process current node
   
   c. For each neighbor of current:
      - If neighbor not visited AND not in queue:
         * Mark as visited
         * Enqueue neighbor

5. End
```

---

### BFS Properties

**1. Completeness**
```
✓ Complete: YES
If solution exists in finite graph, BFS will find it
```

**2. Optimality**
```
✓ Optimal: YES (with conditions)
Conditions:
- Unweighted graph (or all edges have same weight)
- Undirected graph

Guarantees shortest path in terms of number of edges
```

**3. Time Complexity**
```
O(b^d)

Where:
b = Branching factor (average number of children per node)
d = Depth of shallowest goal node
```

**4. Space Complexity**
```
O(b^d)

Reason: Must store all nodes at current level in queue
Worst case: All nodes at deepest level
```

---

### Advantages of BFS

```
✓ Guarantees shortest path (unweighted graphs)
✓ Complete algorithm
✓ Closer nodes discovered before farther ones
✓ Good for finding nearest solution
```

---

### Disadvantages of BFS

```
✗ Inefficient in terms of space (stores many nodes)
✗ Inefficient in terms of time (explores many nodes)
✗ Slow if solution is far from root
✗ Not advisable for weighted graphs
```

**Why Not for Weighted Graphs?**
```
Consider:
A --1--> B --1--> C  (Total: 2)
A --10--> C         (Total: 10)

BFS might choose A→C (one edge)
But A→B→C is actually shorter (cost: 2 vs 10)
```

---

## Depth-First Search (DFS)

### Definition

**What is DFS?**
> "An uninformed search strategy that explores as far as possible along each branch before backtracking"

**Key Concept:**
- Pick a path
- Go as deep as possible
- Backtrack only when no forward option
- Explore other branches

---

### How DFS Works

**Approach:**
1. Start from root node
2. Pick any neighbor (random)
3. Keep going deeper
4. Backtrack when no unvisited neighbors
5. Explore other branches
6. Repeat until all explored

**Data Structure:** Stack (LIFO - Last In First Out)

**Implementation:** Typically uses recursion (implicit stack)

---

### DFS Example - Step by Step

**Given Graph:**
```
    A
   / \
  B   E
  |   |\
  C   D F
  |     |
  G     G
```

**Random path exploration:** A → B → C → E → D → F → G

**Stack Trace:**

```
Step 1: Start at A
Stack: [A]

Step 2: A calls B
Stack: [A, B]

Step 3: B calls C
Stack: [A, B, C]

Step 4: C calls E
Stack: [A, B, C, E]

Step 5: E calls D
Stack: [A, B, C, E, D]

Step 6: D has no unvisited neighbors → Backtrack
Stack: [A, B, C, E]  (D popped)

Step 7: E calls F
Stack: [A, B, C, E, F]

Step 8: F calls G
Stack: [A, B, C, E, F, G]

Step 9-14: Backtrack all the way
Stack pops: G → F → E → C → B → A
```

---

### Opening and Closing Numbers

**Detailed Trace:**

```
Node | Open | Close
-----|------|------
A    |  1   |  14
B    |  2   |  13
C    |  3   |  12
E    |  4   |  11
D    |  5   |   6
F    |  7   |  10
G    |  8   |   9
```

**Interpretation:**
- Opening number: When node is first visited
- Closing number: When all its descendants are explored

---

### DFS Algorithm (Simplified)

```
Algorithm DFS(Graph, node):
1. Mark node as visited
2. Process node

3. For each unvisited neighbor of node:
   a. Recursively call DFS(Graph, neighbor)

4. Backtrack (when no unvisited neighbors)

Base case: No unvisited neighbors
```

**Iterative Version (using explicit Stack):**
```
Algorithm DFS_Iterative(Graph, start):
1. Create empty Stack
2. Push start onto Stack
3. Mark start as visited

4. While Stack is not empty:
   a. Pop top element (current)
   b. Process current
   
   c. For each unvisited neighbor of current:
      - Mark neighbor as visited
      - Push neighbor onto Stack

5. End
```

---

### DFS Properties

**1. Completeness**
```
✗ NOT Complete
Can get trapped in infinite branch with cycles
May never reach goal even if it exists
```

**2. Optimality**
```
✗ NOT Optimal
Does not guarantee shortest path
Depends on order of exploration
```

**3. Time Complexity**
```
O(b^m)

Where:
b = Branching factor
m = Maximum depth of graph/tree
```

**4. Space Complexity**
```
O(bm) or O(m)

Much better than BFS!
Reason: Only stores nodes on current path (not all nodes at level)
```

---

### Advantages of DFS

```
✓ Memory efficient (compared to BFS)
✓ Uses stack (less memory than queue)
✓ Good for exploring one path completely
✓ Better space complexity
```

---

### Disadvantages of DFS

```
✗ Not complete (can get stuck in cycles)
✗ Not optimal (doesn't guarantee shortest path)
✗ May explore very deep before finding solution nearby
✗ Can get trapped in infinite branches
```

**Problem with Cycles:**
```
Graph with cycle:
A → B → C → A → B → C → A ...

DFS might keep circling without finding goal
```

---

### BFS vs DFS Comparison

| Aspect | BFS | DFS |
|--------|-----|-----|
| **Data Structure** | Queue (FIFO) | Stack (LIFO) |
| **Exploration** | Level by level | Deep then backtrack |
| **Complete** | Yes (finite graphs) | No (can loop) |
| **Optimal** | Yes (unweighted) | No |
| **Time Complexity** | O(b^d) | O(b^m) |
| **Space Complexity** | O(b^d) | O(bm) - Better! |
| **Use When** | Shortest path needed | Memory limited |
| **Implementation** | Iterative (queue) | Recursive (stack) |

---

## Uniform Cost Search

### Definition

**What is Uniform Cost Search?**
> "A variant of BFS that considers edge costs and explores nodes in order of increasing path cost from the root"

**Key Difference from BFS:**
```
BFS: All edges cost = 1 (or equal)
UCS: Edges have different costs
```

---

### How UCS Works

**Principle:**
- Not just distance in terms of edges
- Consider actual cost to reach node
- Always expand node with lowest path cost

**Priority:**
> "Explore cheaper paths before expensive ones"

---

### UCS Example

**Given Weighted Graph:**
```
    A
   /|\
  1 6 5
 /  |  \
B   E   C
|   |\  |
2   | 4 1
|   3 | |
D   | F |
    |   |
    D   G
```

**Step-by-Step Exploration:**

```
Start: A (cost: 0)

From A:
├── To B: cost = 1
├── To E: cost = 6
└── To C: cost = 5

Next: B (lowest cost = 1)

From B:
└── To D: cost = 1 + 2 = 3

Current costs:
- D: 3
- C: 5
- E: 6

Next: D (lowest cost = 3)

From D:
└── No new nodes

Next: C (cost = 5)

From C:
├── To F: cost = 5 + 1 = 6
└── To G: cost = 5 + 4 = 9

Current costs:
- F: 6
- E: 6
- G: 9

Next: E or F (both cost 6, choose F)

And so on...
```

**Order of Exploration:**
```
A (0) → B (1) → D (3) → C (5) → F (6) → E (7) → ...
```

---

### Implementation

**Data Structure:** Priority Queue (Min-Heap)

**Why Priority Queue?**
- Always extract node with minimum cost
- Efficient for cost-based exploration

**Algorithm:**
```
Algorithm UCS(Graph, start, goal):
1. Create Priority Queue
2. Insert (start, cost=0)
3. Create empty visited set

4. While Priority Queue not empty:
   a. Extract node with minimum cost
   b. If node == goal: return path
   
   c. If node not visited:
      - Mark as visited
      - For each neighbor:
         * Calculate new_cost = current_cost + edge_cost
         * Insert (neighbor, new_cost) into queue

5. Return "No path found"
```

---

### UCS Properties

**1. Completeness**
```
✓ Complete: YES
Will find solution if it exists
```

**2. Optimality**
```
✓ Optimal: YES
Guaranteed to find least-cost path
```

**3. Time Complexity**
```
O(b^d)

But explores nodes in order of cost
May be better or worse than BFS depending on graph
```

**4. Space Complexity**
```
O(b^d)

Similar to BFS
```

---

### Advantages of UCS

```
✓ Optimal solution guaranteed
✓ Considers edge costs
✓ Better than BFS for weighted graphs
✓ Complete algorithm
```

---

### Disadvantages of UCS

```
✗ More complex than BFS
✗ Requires priority queue
✗ Still can be slow
✗ No heuristic guidance
```

---

## Bidirectional Search

### Definition

**What is Bidirectional Search?**
> "Simultaneously searches from both start node toward goal and from goal node toward start, meeting in the middle"

**Core Idea:**
```
Instead of: Start → → → → → Goal

Do both:
Start → → →     ← ← ← Goal
         ↓
      Meet here
```

---

### Why Bidirectional Search?

**Problem with Regular Search:**
```
Complexity: O(b^d)

Where:
b = Branching factor (cannot change)
d = Depth (can reduce!)
```

**Bidirectional Solution:**
```
Both searches go half the depth:

Forward search: d/2
Backward search: d/2

Total: b^(d/2) + b^(d/2) = 2 × b^(d/2)

This is MUCH less than b^d!
```

---

### Mathematical Advantage

**Example:**
```
Assume b = 10, d = 6

Regular search: 10^6 = 1,000,000 nodes

Bidirectional:
├── Forward: 10^3 = 1,000 nodes
├── Backward: 10^3 = 1,000 nodes
└── Total: 2,000 nodes

Reduction: 1,000,000 → 2,000 (500x improvement!)
```

---

### How It Works

**Process:**
```
1. Start two simultaneous searches:
   ├── Forward: From start toward goal
   └── Backward: From goal toward start

2. Continue both until they meet

3. When searches intersect:
   └── Combine paths
   └── Return complete solution
```

**Real-World Analogy: Tunnel Digging**
```
Mountain tunnel:
├── Team A digs from left side
├── Team B digs from right side
└── Meet in middle (faster than one team)
```

---

### Critical Requirement

**Must Ensure Intersection:**
```
Problem:
├── Forward search goes one direction
├── Backward search goes different direction
└── They never meet!

Solution:
├── Both must use same search strategy
├── Must coordinate and synchronize
└── Check for intersection at each step
```

---

### Bidirectional Search Properties

**1. Completeness**
```
✓ Complete: YES
If solution exists, will find it
```

**2. Optimality**
```
✓ Optimal: YES
Both searches guarantee optimality
```

**3. Time Complexity**
```
O(b^(d/2))

MUCH better than O(b^d)!
```

**4. Space Complexity**
```
O(b^(d/2))

But requires memory for BOTH searches
So effectively: 2 × b^(d/2)
Still better than b^d overall
```

---

### Advantages

```
✓ Faster exploration
✓ Reduced effective branching factor
✓ Significantly reduced time complexity
✓ Optimal solution
```

---

### Disadvantages

```
✗ Additional coordination overhead
✗ Both searches must synchronize
✗ Higher memory requirement (two searches)
✗ More complex implementation
```

---

## Comparison Summary

### All Uninformed Search Algorithms

| Algorithm | Complete | Optimal | Time | Space | Notes |
|-----------|----------|---------|------|-------|-------|
| **BFS** | Yes | Yes* | O(b^d) | O(b^d) | *Only for unweighted graphs |
| **DFS** | No | No | O(b^m) | O(bm) | Can get stuck in cycles |
| **UCS** | Yes | Yes | O(b^d) | O(b^d) | Considers edge costs |
| **Bidirectional** | Yes | Yes | O(b^(d/2)) | O(b^(d/2)) | Best time complexity |

**Key:**
- b = Branching factor
- d = Depth of shallowest goal
- m = Maximum depth

---

### When to Use Which Algorithm?

**Use BFS When:**
```
✓ Need shortest path (unweighted graph)
✓ Goal is not far from start
✓ Graph is unweighted
✓ Memory is not a constraint
```

**Use DFS When:**
```
✓ Memory is limited
✓ Graph has many long paths
✓ Solution is likely to be deep
✓ Optimality not required
```

**Use UCS When:**
```
✓ Graph has different edge costs
✓ Need optimal solution
✓ Weighted graph
✓ Cost matters more than edges
```

**Use Bidirectional When:**
```
✓ Both start and goal are known
✓ Need fast solution
✓ Can coordinate both searches
✓ Branching factor is high
```

---

## Detailed Comparison Table

### Completeness

| Algorithm | Complete? | Conditions |
|-----------|-----------|------------|
| BFS | ✓ Yes | Finite graph |
| DFS | ✗ No | Can loop infinitely |
| UCS | ✓ Yes | Finite graph |
| Bidirectional | ✓ Yes | Both searches intersect |

---

### Optimality

| Algorithm | Optimal? | Conditions |
|-----------|----------|------------|
| BFS | ✓ Yes | Unweighted/equal-cost edges |
| DFS | ✗ No | Explores arbitrarily |
| UCS | ✓ Yes | Always optimal |
| Bidirectional | ✓ Yes | If both use optimal strategy |

---

### Complexity Comparison

**Assuming b=10, d=5:**

| Algorithm | Time Nodes | Space Nodes |
|-----------|------------|-------------|
| BFS | 10^5 = 100,000 | 100,000 |
| DFS | 10^m (depends) | 10×m (much less) |
| UCS | ~100,000 | ~100,000 |
| Bidirectional | 2×10^2.5 ≈ 633 | ~633 |

**Clear Winner for Time:** Bidirectional

**Clear Winner for Space:** DFS

---

## Key Takeaways

### Must Remember Points

**1. Search Types:**
```
Uninformed Search:
└── No domain knowledge
└── Examples: BFS, DFS, UCS, Bidirectional

Informed Search:
└── Uses heuristics
└── Examples: Best-First, A*, Hill Climbing
```

**2. BFS vs DFS:**
```
BFS:
├── Queue (FIFO)
├── Level by level
└── Optimal for unweighted

DFS:
├── Stack (LIFO)
├── Deep exploration
└── Memory efficient
```

**3. Important Formulas:**
```
Time Complexity: O(b^d)
Space Complexity: O(b^d) for BFS, O(bm) for DFS
Bidirectional: O(b^(d/2))
```

---

### Exam Tips

**For 5-10 Mark Questions:**

**1. Write Comparison Table**
- Easier for examiner to read
- Clear presentation
- Covers multiple points quickly

**2. Draw Diagrams**
- BFS and DFS traversal diagrams
- Show step-by-step execution
- Diagrams worth significant marks

**3. Include:**
- Algorithm (pseudo-code)
- Example with graph
- Advantages and disadvantages
- Complexity analysis
- Properties (complete, optimal)

**4. Common Question Types:**
```
Q1: Explain BFS with example (5-7 marks)
Q2: Compare BFS and DFS (5 marks)
Q3: Write algorithm for DFS (3-5 marks)
Q4: Advantages and disadvantages of UCS (5 marks)
```

---

## Next Topics

**Informed Search Algorithms (Coming Next):**
1. Best-First Search
2. A* Algorithm
3. AO* Algorithm
4. Hill Climbing

These use heuristics and domain knowledge for more efficient search.

---

## Quick Reference

### Algorithm Selection Guide

```
Given: Unweighted graph, need shortest path
→ Use: BFS

Given: Weighted graph, need optimal path
→ Use: UCS

Given: Limited memory
→ Use: DFS

Given: Known start and goal, need fast result
→ Use: Bidirectional

Given: Have heuristic information
→ Use: Informed Search (Next chapter)
```

### Complexity Quick Reference

```
BFS:  Time O(b^d), Space O(b^d)
DFS:  Time O(b^m), Space O(bm)
UCS:  Time O(b^d), Space O(b^d)
Bid:  Time O(b^(d/2)), Space O(b^(d/2))
```
