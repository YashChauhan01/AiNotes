# Informed Search (Heuristic Search) Algorithms - Complete Notes

## Table of Contents
1. [Introduction to Informed Search](#introduction)
2. [Heuristic Functions](#heuristic-functions)
3. [Best-First Search](#best-first-search)
4. [A* Algorithm](#a-star-algorithm)
5. [Admissibility and Consistency](#admissibility-and-consistency)
6. [AO* Algorithm](#ao-star-algorithm)
7. [Comparison Summary](#comparison-summary)

---

## Introduction to Informed Search

### What is Informed Search?

**Also Known As:**
- Heuristic Search
- Smart Search Methods

**Real-World Analogy:**
```
Scenario: Lost in a city, need to find Taj Mahal

Uninformed Approach:
└── Wander randomly, explore entire city

Informed Approach:
└── Ask locals for directions (use clues/hints)
└── Reach faster using information
```

---

### Core Concept

**Definition:**
> "Smart search methods that use special knowledge and hints to find solutions more effectively"

**Key Idea:**
- Use heuristics (clues/estimates) to guide search
- Don't explore entire problem space
- Reach solution faster (usually)
- Similar to using intuition and common sense

---

### Important Distinction

**Does NOT Always Guarantee:**
```
✗ Optimal solution
✗ Best possible answer

Success HEAVILY depends on:
└── Quality of heuristic
└── Accuracy of information
```

**Real-World Example:**
```
Good Directions:
"Go straight, take left, you'll find it"
→ Fast arrival

Confusing Directions:
Person is confused, gives wrong info
→ May take longer than exploring yourself!
```

---

### Quality vs Speed Trade-off

**What Informed Search Provides:**
```
✓ Good solutions (usually)
✓ Sometimes optimal
✓ Often close to optimal
✓ Much faster than uninformed search
✓ Less space required
```

**Why Faster?**
- Doesn't explore every path
- Uses guidance to choose promising paths
- Avoids exhaustive search

---

## Heuristic Functions

### What is a Heuristic Function?

**Notation:** h(n)

**Definition:**
> "An estimate of the cost from a node to the goal"

**Key Characteristics:**
```
1. It's an ESTIMATE (not exact)
2. May overestimate or underestimate
3. Helps guide search decisions
4. Domain-specific knowledge
```

---

### Example: Straight-Line Distance

**Common Heuristic for Graph Problems:**
```
Straight-Line Distance (SLD)

Example: Delhi to Mumbai
├── Straight line on map: 1000 km (estimate)
├── Actual road distance: 1200 km (real)
└── Why difference? Roads aren't straight
    (go through Jaipur, Kota, Surat, etc.)
```

**Properties:**
```
✓ Easy to calculate
✓ Never overestimates (actual path always longer)
✓ Good guidance for search
```

---

### How Heuristics are Obtained

**Common Methods:**
1. **Straight-line distance** (geographical problems)
2. **Manhattan distance** (grid-based problems)
3. **Domain knowledge** (expert information)
4. **Relaxed problem solutions** (ignoring constraints)
5. **Pattern databases** (precomputed estimates)

---

## Best-First Search

### Core Idea

**Principle:**
> "Explore the most promising node based ONLY on heuristic estimate"

**Key Feature:**
```
Ignores actual cost incurred so far
Uses ONLY heuristic estimate h(n)
```

---

### Best-First Search Example

**Given Graph:**
```
Nodes with heuristic values h(n):
A: 39, B: 31, C: 24, D: 34, E: 18, F: 16, G: 0

Edge costs exist but are IGNORED in Best-First Search
```

**Step-by-Step Execution:**

```
Step 1: Start at A
Options from A:
├── To D: h(D) = 34
├── To C: h(C) = 24 ← BEST (lowest)
└── To B: h(B) = 31

Choose: C (h = 24)

Step 2: From C
Options from C:
├── To E: h(E) = 18
└── To F: h(F) = 16 ← BEST

Choose: F (h = 16)

Step 3: From F
Only option:
└── To G: h(G) = 0 (goal!)

Solution Path: A → C → F → G
```

**Note:** Edge costs between nodes were completely ignored!

---

### Best-First Search Algorithm

```
Algorithm Best_First_Search(start, goal):
1. Create priority queue (ordered by h(n))
2. Insert start node
3. Mark start as visited

4. While queue not empty:
   a. Remove node with lowest h(n)
   b. If node == goal: return path
   
   c. For each neighbor:
      - Calculate h(neighbor)
      - If not visited:
         * Add to priority queue
         * Mark as visited

5. Return failure
```

---

### Best-First Search Properties

**1. Completeness**
```
✗ NOT Complete
Can get stuck in loops (directed graphs)
```

**2. Optimality**
```
✗ NOT Optimal
May find good solution
Sometimes finds optimal
NO guarantee
```

**3. Time Complexity**
```
Worst case: O(b^d)

But practically:
Much better than BFS/DFS
Doesn't explore entire graph
```

**4. Space Complexity**
```
Relatively low
Only stores promising paths
```

---

### Advantages

```
✓ Fast exploration
✓ Doesn't explore entire graph
✓ Low memory requirement
✓ Simple calculations (just compare h values)
✓ No arithmetic operations needed
```

---

### Disadvantages

```
✗ NOT complete (can loop)
✗ NOT optimal (no guarantee)
✗ Quality depends entirely on heuristic
✗ Bad heuristic → Bad solution
```

---

## A* Algorithm

### Core Idea

**Improvement Over Best-First Search:**
```
Best-First Search: Only uses h(n) (estimate)
A*: Uses f(n) = g(n) + h(n)

Where:
g(n) = Actual cost from start to n (EXACT)
h(n) = Estimated cost from n to goal (HEURISTIC)
f(n) = Total estimated cost of path through n
```

**Balance:**
- Considers actual cost incurred (like Dijkstra, Bellman-Ford)
- Also considers estimated future cost (like Best-First)
- Best of both worlds!

---

### A* Formula

```
f(n) = g(n) + h(n)

f(n) = Total estimated cost
g(n) = Actual cost to reach n (from graph edges)
h(n) = Heuristic estimate (n to goal)
```

---

### A* Example - Step by Step

**Given Graph:**
```
Edges with actual costs + Heuristic values

Example:
A: h=14    A→B: 4    A→C: 3
B: h=12    B→E: 10   
C: h=11    C→D: 7    C→E: 10
D: h=6     D→F: 2
E: h=4     E→F: 5
F: h=0     F→Z: 5
Z: h=0 (goal)
```

---

**Step 1: Start at A**

From A, can go to B or C

**Calculate f(B):**
```
g(B) = Cost to reach B = 4
h(B) = Heuristic of B = 12
f(B) = g(B) + h(B) = 4 + 12 = 16
```

**Calculate f(C):**
```
g(C) = Cost to reach C = 3
h(C) = Heuristic of C = 11
f(C) = g(C) + h(C) = 3 + 11 = 14
```

**Decision:** Choose C (f = 14 < 16)

**Path so far:** A → C

---

**Step 2: From C**

From C, can go to D or E

**Calculate f(D):**
```
g(D) = Cost to reach D = 3 + 7 = 10
h(D) = 6
f(D) = 10 + 6 = 16
```

**Calculate f(E):**
```
g(E) = Cost to reach E = 3 + 10 = 13
h(E) = 4
f(E) = 13 + 4 = 17
```

**Decision:** Choose D (f = 16 < 17)

**Path so far:** A → C → D

---

**Step 3: From D**

Only one option: D → F

```
g(F) = 10 + 2 = 12
h(F) = 0
f(F) = 12 + 0 = 12
```

**Step 4: From F**

Only one option: F → Z (goal)

```
Final Path: A → C → D → F → Z
Total Cost: 3 + 7 + 2 + 5 = 17
```

---

### A* Algorithm (Simplified)

```
Algorithm A_Star(start, goal):
1. Create priority queue (ordered by f(n))
2. Insert start with f(start) = g(start) + h(start)
3. Create visited set

4. While queue not empty:
   a. Remove node with lowest f(n)
   b. If node == goal: return path
   
   c. Mark node as visited
   
   d. For each neighbor:
      - Calculate g(neighbor) = g(node) + cost(node, neighbor)
      - Calculate f(neighbor) = g(neighbor) + h(neighbor)
      - If neighbor not visited:
         * Add to priority queue with f value

5. Return failure
```

---

### A* Properties

**1. Completeness**
```
✓ Complete (if search space finite and h is admissible)
```

**2. Optimality**
```
✓ Optimal (if h is admissible and consistent)
```

**3. Time Complexity**
```
Worst case: O(b^d)

Practically:
Better than Best-First Search
Still depends on heuristic quality
```

**4. Space Complexity**
```
Similar to BFS: O(b^d)
More than Best-First Search
But worth it for optimality guarantee
```

---

### Advantages

```
✓ Optimal solution (with conditions)
✓ Complete (with conditions)
✓ Much better than uninformed search
✓ Balances actual and estimated costs
✓ Industry standard for pathfinding
```

---

### Disadvantages

```
✗ More complex than Best-First
✗ More calculations required
✗ Higher memory requirement
✗ Still depends on heuristic quality
```

---

## Admissibility and Consistency

### Two Critical Conditions for A* Optimality

```
1. Admissibility
2. Consistency
```

---

### Admissibility

**Definition:**
> "A heuristic h(n) is admissible if it NEVER overestimates the cost to reach the goal"

**Formula:**
```
h(n) ≤ h*(n)

Where:
h(n) = Heuristic estimate
h*(n) = True optimal cost to goal
```

**In Simple Terms:**
```
Always estimate LESS than or EQUAL to actual cost
NEVER estimate MORE

Example:
Actual cost: 10
✓ Estimate: 6 (admissible)
✓ Estimate: 8 (admissible)
✓ Estimate: 10 (admissible)
✗ Estimate: 12 (NOT admissible - overestimate)
✗ Estimate: 15 (NOT admissible)
```

---

**Why Admissibility Matters:**
```
Admissible heuristic = Optimistic
Always thinks cost is less than actual

Result:
→ Won't miss optimal path
→ Won't prematurely abandon good paths
```

**Example: Straight-Line Distance**
```
✓ Always admissible

Reason:
Straight line is shortest possible distance
Actual path must be ≥ straight line
Never overestimates
```

---

### Consistency (Monotonicity)

**Definition:**
> "For every node n and successor n', the estimated cost from n to goal is no greater than the step cost to n' plus the estimated cost from n' to goal"

**Formula:**
```
h(n) ≤ cost(n, n') + h(n')

Where:
n = Current node
n' = Successor of n
cost(n, n') = Actual edge cost
h(n) = Heuristic from n to goal
h(n') = Heuristic from n' to goal
```

---

**Triangle Inequality:**
```
    n -----> n'
    |         |
    |         |
    ↓         ↓
   Goal     Goal

Direct estimate from n: h(n)
Via n': cost(n,n') + h(n')

Consistency: h(n) ≤ cost(n,n') + h(n')
```

**In Simple Terms:**
```
Going via n' should not appear cheaper than direct estimate
Otherwise, our estimates are inconsistent
```

---

**Example:**

```
Nodes:
n: h(n) = 10
n': h(n') = 6
Edge: cost(n, n') = 3

Check consistency:
h(n) ≤ cost(n, n') + h(n')
10 ≤ 3 + 6
10 ≤ 9 ??? NO!

This is INCONSISTENT
```

**Fixed Example:**
```
n: h(n) = 7
n': h(n') = 6
Edge: cost(n, n') = 3

Check:
7 ≤ 3 + 6
7 ≤ 9 ✓ YES

This is CONSISTENT
```

---

### Relationship Between Properties

```
Consistency → Admissibility
(If consistent, then admissible)

But NOT vice versa:
Admissible ≠ Consistent necessarily
```

**Why Consistency Matters:**
```
With consistent heuristic:
✓ A* is optimal
✓ First path to goal is optimal
✓ No need to revisit nodes
✓ More efficient
```

---

### Summary Table

| Property | Condition | Result |
|----------|-----------|--------|
| **Admissible** | h(n) ≤ h*(n) | A* finds optimal solution |
| **Consistent** | h(n) ≤ c(n,n') + h(n') | A* more efficient + optimal |
| **Both** | Both conditions met | Best A* performance |

---

## AO* Algorithm

### Key Difference from A*

**A* Algorithm:**
```
Works on: OR graphs
Choice: Pick ONE path from multiple options
```

**AO* Algorithm:**
```
Works on: AND-OR graphs
Must solve: ALL subproblems in AND nodes
```

---

### What is an AND-OR Graph?

**OR Arc (Normal):**
```
Choose ONE option:

Problem: Get a phone
Option 1: Steal a phone (cost: 4)
      OR
Option 2: Earn money AND purchase (cost: 11)
```

**AND Arc:**
```
Must solve BOTH:

Problem: Get phone by earning
├── Subproblem 1: Earn money (cost: 10)
└── Subproblem 2: Purchase phone (cost: 1)

Total cost = 10 + 1 = 11 (sum both)
```

---

### AND-OR Graph Notation

```
Regular edge:     A → B (OR - choose one)

AND arc:         A → B
                  ↘ C   (must solve both B AND C)
                  
Visual: Curved line connecting edges
```

---

### When to Use AO*

**Use Case:**
> "Problems that can be solved by decomposing them into a set of smaller subproblems, where ALL must be solved"

**Examples:**
```
1. Planning problems with subgoals
2. Game playing with multiple objectives
3. Robot task planning (must complete all subtasks)
```

---

### AO* Example - Step by Step

**Given AND-OR Graph:**

```
       A (h=2)
      / | \
     /  |  \
   OR  AND  
   /    |\   
  B(4) C(2) D(3)
  /|\   |    |
 E F  G(1) H(1)
(6)(8)

Legend:
- Single line = OR (choose one)
- Curved line = AND (solve both)
- Numbers in () = heuristic values
- Edge costs = 1 (uniform)
```

---

**Bottom-Up Calculation:**

**Step 1: Evaluate B**
```
From B, two OR options:
├── Via E: 1 (edge) + 6 (h) = 7
└── Via F: 1 (edge) + 8 (h) = 9

Best: 7 (via E)
Update h(B) = 7
```

**Step 2: Evaluate C and D (AND arc)**
```
From C:
└── Via G: 1 + 1 = 2

From D:
└── Via H: 1 + 1 = 2

Since AND arc:
Total = 2 + 2 = 4

But previous h(C) = 2, h(D) = 3
Updated costs are used
```

**Step 3: Evaluate A**
```
Option 1: Via B
Cost = 1 + 7 = 8

Option 2: Via C AND D
Cost = 1 + (updated h(C)) + 1 + (updated h(D))
     = 1 + 3 + 1 + 2 = 7

Best: 7 (via C and D)
```

**Solution:**
```
Solve A by:
├── Solving C via G
└── Solving D via H

Path: A → {C → G, D → H}
```

---

### AO* Algorithm (Simplified)

```
Algorithm AO_Star(root):
1. Initialize all nodes with heuristic values
2. Start from root, expand top-down
3. For each node:
   a. If leaf: use given heuristic
   b. If OR node: choose minimum cost child
   c. If AND node: sum all children costs
4. Propagate costs bottom-up
5. Update heuristics if actual cost differs
6. Mark solution path
7. Repeat until goal reached
```

---

### AO* Properties

**1. Completeness**
```
✓ Complete
If solution exists, will find it
```

**2. Optimality**
```
✓ Optimal
Finds optimal solution with admissible heuristic
```

**3. Time Complexity**
```
Depends on:
├── Heuristic quality
├── Branching factor
└── Problem structure
```

**4. Space Complexity**
```
Similar to A*
Can be high
```

---

### Advantages

```
✓ Handles AND-OR graphs
✓ Optimal solution guaranteed
✓ Can decompose complex problems
✓ Updates estimates during search
```

---

### Disadvantages

```
✗ High memory consumption
✗ More complex than A*
✗ Performance depends on heuristic quality
✗ Requires admissibility
```

---

## Comparison Summary

### All Informed Search Algorithms

| Algorithm | Uses | Optimality | Completeness | Complexity |
|-----------|------|------------|--------------|------------|
| **Best-First** | h(n) only | No | No | Low |
| **A*** | g(n) + h(n) | Yes* | Yes* | Medium |
| **AO*** | AND-OR graphs | Yes* | Yes | High |

**\*With admissible (and consistent for A*) heuristic**

---

### Detailed Comparison

**Best-First Search:**
```
Formula: f(n) = h(n)
Uses: Only heuristic estimate
Ignores: Actual cost incurred
Speed: Fastest
Optimality: No guarantee
Best for: Quick approximations
```

**A* Search:**
```
Formula: f(n) = g(n) + h(n)
Uses: Actual cost + heuristic
Balances: Both components
Speed: Moderate
Optimality: Yes (with conditions)
Best for: Finding optimal paths
```

**AO* Search:**
```
Formula: Similar to A*, but with AND-OR
Uses: Problem decomposition
Handles: Subgoal structures
Speed: Slower than A*
Optimality: Yes (with conditions)
Best for: Planning problems
```

---

### When to Use Each Algorithm

**Use Best-First Search:**
```
✓ Need fast approximate solution
✓ Optimality not critical
✓ Have good heuristic
✓ Limited computational resources
```

**Use A* Search:**
```
✓ Need optimal solution
✓ Have admissible heuristic
✓ OR graph problem
✓ Pathfinding scenarios
```

**Use AO* Search:**
```
✓ Problem has subgoals
✓ Must solve multiple subtasks
✓ AND-OR graph structure
✓ Planning and decomposition needed
```

---

## Key Formulas Summary

### Heuristic Function
```
h(n) = Estimated cost from n to goal
```

### Best-First Search
```
f(n) = h(n)
Expand node with minimum h(n)
```

### A* Search
```
f(n) = g(n) + h(n)

Where:
g(n) = Actual cost from start to n
h(n) = Estimated cost from n to goal
f(n) = Total estimated cost
```

### Admissibility
```
h(n) ≤ h*(n)
Never overestimate
```

### Consistency
```
h(n) ≤ cost(n, n') + h(n')
Triangle inequality
```

---

## Important Concepts Recap

### 1. Heuristic Quality is Critical

```
Good Heuristic:
├── Accurate estimates
├── Admissible (doesn't overestimate)
├── Informative (guides well)
└── Result: Fast, optimal solution

Bad Heuristic:
├── Inaccurate estimates
├── May overestimate
├── Misleading
└── Result: Slow, suboptimal solution
```

---

### 2. Under-estimation vs Over-estimation

```
Under-estimation (Good):
├── h(n) < actual cost
├── Admissible
├── May explore more nodes
└── But won't miss optimal

Over-estimation (Bad):
├── h(n) > actual cost
├── NOT admissible
├── May explore fewer nodes
└── But might miss optimal path
```

---

### 3. Trade-offs

```
Speed vs Optimality:
├── Best-First: Fast, not optimal
├── A*: Moderate, optimal
└── AO*: Slower, optimal for AND-OR

Memory vs Quality:
├── More memory → Better solutions
└── Less memory → Approximate solutions
```

---

## Exam Tips

### Must Remember

**1. Key Differences:**
```
Best-First:  Only h(n)
A*:          g(n) + h(n)
AO*:         AND-OR graphs
```

**2. Admissibility:**
```
Never overestimate
h(n) ≤ actual cost
Required for A* optimality
```

**3. Common Questions:**
```
Q1: Solve graph using Best-First Search
Q2: Solve graph using A*
Q3: Explain admissibility
Q4: Compare Best-First vs A*
Q5: When to use AO*?
```

---

### Answer Writing Strategy

**For Graph Problem (10 marks):**

```
1. Show step-by-step calculation
2. At each node, clearly show:
   - For Best-First: h(n) values
   - For A*: g(n), h(n), f(n) values
3. Circle/highlight chosen nodes
4. Draw final path
5. Write total cost
6. Brief conclusion
```

**Example Format:**
```
Step 1: At A
├── f(B) = g(B) + h(B) = 4 + 12 = 16
└── f(C) = g(C) + h(C) = 3 + 11 = 14 ← Choose

Step 2: At C
...
```

---

## Quick Reference

### Algorithm Selection Guide

```
Need: Fast approximate solution
→ Use: Best-First Search

Need: Optimal path, have admissible h
→ Use: A* Search

Need: Solve subproblems, AND-OR structure
→ Use: AO* Search

Have: Only heuristic, no edge costs
→ Use: Best-First Search

Have: Both edge costs and heuristic
→ Use: A* Search
```

---

### Common Heuristics

```
Geographical Problems:
└── Straight-line distance (SLD)

Grid Problems:
└── Manhattan distance

Puzzle Problems:
└── Number of misplaced tiles

General:
└── Relaxed problem solution
```

---

## Final Summary

**Core Principle:**
> "Use information/heuristics to guide search toward goal, rather than blind exploration"

**Success Factors:**
```
1. Quality of heuristic
2. Admissibility of heuristic
3. Problem structure
4. Available resources
```

**Main Advantage:**
```
Much faster than uninformed search
Often finds good/optimal solutions
```

**Main Risk:**
```
Bad heuristic → Bad results
Quality depends heavily on h(n)
```
