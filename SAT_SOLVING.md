# SAT Solving Course - Oral Exam Preparation Guide
**Course: 184.090 VU SAT Solving - TU Wien**
**Professor: Katalin Fazekas**

---

## CRITICAL: Your Project Clarification

### What You Actually Implemented
- **NOT:** Classical CNF vivification with BCP
- **ACTUALLY:** Constraint-level pattern-based redundancy elimination
- **Level:** Semantic/first-order constraints, not propositional CNF
- **Method:** String pattern matching, not Boolean Constraint Propagation

### Honest Assessment
**Strengths:**
- Real preprocessing (39.4% reduction)
- 100% correctness preservation
- Working integration with modern framework

**Weaknesses:**
- Misrepresented as "vivification"
- Wrong abstraction level for Algorithm 3
- Should have worked on CNF benchmarks

### How to Frame It
"I implemented constraint-level preprocessing inspired by vivification principles. While Algorithm 3 operates on CNF with BCP, my work adapted the redundancy-removal concept to Logic-LLM's higher semantic level using pattern matching. I should have been clearer this was principle-inspired, not a faithful implementation."

---

## Topic 1: Boolean Satisfiability (SAT) Basics

### What is SAT?
Given a Boolean formula, does there exist an assignment making it TRUE?

**Formula:** F = (x₁ ∨ ¬x₂) ∧ (x₂ ∨ x₃) ∧ (¬x₁ ∨ ¬x₃)
**Question:** Can we assign x₁, x₂, x₃ to make F = TRUE?
**Answer:** YES (e.g., x₁=T, x₂=T, x₃=F) → SAT

### Key Concepts
- **SAT:** Satisfiable - solution exists
- **UNSAT:** Unsatisfiable - no solution
- **NP-Complete:** Hard in worst case, but practical solvers work well
- **Applications:** Verification, planning, scheduling, AI reasoning

### CNF (Conjunctive Normal Form)
**Structure:** AND of ORs
- **Literal:** Variable (x) or negation (¬x)
- **Clause:** Disjunction of literals (x₁ ∨ ¬x₂ ∨ x₃)
- **CNF Formula:** Conjunction of clauses (C₁ ∧ C₂ ∧ ... ∧ Cₙ)

**Example:**
```
(x ∨ y) ∧ (¬x ∨ z) ∧ (¬y ∨ ¬z)
```

### Why CNF?
- Standard input format for SAT solvers
- Efficient data structures (watched literals)
- Simplifies conflict analysis in CDCL

---

## Topic 2: DPLL Algorithm

### Core Idea
Systematic search with unit propagation and pure literal elimination.

### Algorithm Steps
```
DPLL(F):
  1. If F is empty → return SAT
  2. If F contains empty clause → return UNSAT
  3. Unit propagation: if (ℓ) exists, assign ℓ=TRUE
  4. Pure literal elimination: if ℓ only appears positive/negative, assign
  5. Choose unassigned variable x
  6. If DPLL(F ∧ x) = SAT → return SAT
  7. Else return DPLL(F ∧ ¬x)
```

### Key Components

**Unit Propagation:**
- Unit clause = single literal clause (ℓ)
- Must assign ℓ=TRUE to satisfy
- Propagate: simplify formula with this assignment

**Pure Literal:**
- Variable appears only positive OR only negative
- Safe to assign to satisfy all occurrences

**Backtracking:**
- Try assignment, if conflict → backtrack
- Try opposite assignment

### Example Trace
```
F = (x ∨ y) ∧ (¬x ∨ z) ∧ (¬y) ∧ (¬z ∨ w)

1. Unit clause (¬y) → y=FALSE
2. Simplify: (x) ∧ (¬x ∨ z) ∧ (¬z ∨ w)
3. Unit clause (x) → x=TRUE
4. Simplify: (z) ∧ (¬z ∨ w)
5. Unit clause (z) → z=TRUE
6. Simplify: (w)
7. Unit clause (w) → w=TRUE
8. All clauses satisfied → SAT
```

### Limitations
- No learning from conflicts
- Repeats mistakes
- Exponential worst case

---

## Topic 3: CDCL (Conflict-Driven Clause Learning)

### Key Innovation
**Learn from conflicts** to avoid repeating mistakes.

### CDCL vs DPLL
| DPLL | CDCL |
|------|------|
| Backtrack chronologically | Backjump to conflict cause |
| Forget conflicts | Learn conflict clauses |
| No restart | Strategic restarts |
| Slower | Much faster (modern solvers) |

### Core Components

**1. Decision Levels**
Track when each variable was assigned:
```
Level 0: Initial unit propagations
Level 1: First decision + propagations
Level 2: Second decision + propagations
...
```

**2. Implication Graph**
Shows why variables were assigned:
```
Decision: x₁ @ level 1
   → Propagates: x₃ (from clause C₁)
   → Propagates: x₅ (from clause C₂)
Conflict at x₇!
```

**3. Conflict Analysis**
When conflict occurs:
- Build implication graph backward
- Find **1-UIP (First Unique Implication Point)**
- Learn **conflict clause** that prevents this path
- Backjump to appropriate level

**4. Clause Learning**
```
Conflict: Both x and ¬x derived
Analyze: Why did this happen?
Learn: Add clause preventing this assignment sequence
Result: Prune search space permanently
```

### Example
```
F = (x ∨ y) ∧ (¬x ∨ z) ∧ (¬y ∨ ¬z) ∧ (¬z ∨ w)

Decision: x=TRUE @ level 1
Propagate: z=TRUE (from clause 2)
Propagate: ¬y=TRUE (from clause 3)
Conflict: Clause 1 needs y=TRUE but we have y=FALSE

Analysis: x=TRUE led to conflict
Learn clause: (¬x) 
Backjump: Level 0, assign x=FALSE
Continue solving...
```

### Modern CDCL Features
- **Watched literals:** Efficient unit propagation
- **VSIDS heuristic:** Variable selection based on conflict activity
- **Restarts:** Escape bad search branches
- **Clause deletion:** Remove useless learned clauses

---

## Topic 4: Boolean Constraint Propagation (BCP)

### Definition
Iteratively derive forced assignments from current partial assignment.

### How BCP Works
```
Given partial assignment α and formula F:

1. Find all unit clauses under α
2. For each unit clause (ℓ):
   - Assign ℓ = TRUE
   - Add to α
3. Simplify F with new assignments
4. Repeat until:
   - No more unit clauses (done)
   - Empty clause found (conflict)
```

### Example
```
F = (x₁ ∨ x₂) ∧ (¬x₁ ∨ x₃) ∧ (¬x₂ ∨ ¬x₃) ∧ (x₁)

BCP Process:
1. Unit clause: (x₁) → assign x₁=TRUE
2. After x₁=TRUE: (x₂) ∧ (x₃) ∧ (¬x₂ ∨ ¬x₃)
3. Unit clause: (x₂) → assign x₂=TRUE
4. After x₂=TRUE: (x₃) ∧ (¬x₃)
5. Unit clause: (x₃) → assign x₃=TRUE
6. After x₃=TRUE: () [empty clause]
7. CONFLICT detected!
```

### BCP in Vivification
Algorithm 3 uses BCP to detect redundancy:
```
For clause C = (ℓ₁ ∨ ℓ₂ ∨ ℓ₃):
  Apply BCP with (¬ℓ₁) ∧ (¬ℓ₂) on F\C
  If conflict → C is redundant
  If ¬ℓ₃ propagated → can remove ℓ₃ from C
```

### Watched Literals Optimization
Modern implementation:
- Each clause watches 2 unassigned literals
- Only check clause when watched literal assigned
- O(1) amortized per assignment vs O(n) naive

---

## Topic 5: Preprocessing Techniques

### Purpose
Simplify formula **before** main solving to reduce search space.

### Common Techniques

**1. Subsumption**
Clause C₁ subsumes C₂ if C₁ ⊆ C₂
```
C₁ = (x ∨ y)
C₂ = (x ∨ y ∨ z)
→ Remove C₂ (redundant)
```

**2. Variable Elimination (VE)**
Eliminate variable by resolution:
```
Eliminate x from:
  (x ∨ a) ∧ (¬x ∨ b)
Result:
  (a ∨ b)
```

**3. Blocked Clause Elimination (BCE)**
Clause C is blocked on literal ℓ if:
- ℓ ∈ C
- For all clauses D with ¬ℓ ∈ D: resolvent is tautology

Can remove blocked clauses safely.

**4. Failed Literal Detection**
If setting ℓ=TRUE causes immediate conflict:
- ℓ is "failed literal"
- Can add unit clause (¬ℓ)

**5. Vivification (Algorithm 3)**
Remove/shorten redundant clauses using BCP:
```
for all C = {ℓ₁,...,ℓₙ} in F do
  for all i = 1...n-1 do
    A = BCP(¬ℓ₁,...,¬ℓᵢ, F\C)
    if conflict or ℓⱼ ∈ A with j > i then
      Remove/shorten C
```

### Preprocessing vs Inprocessing
- **Preprocessing:** Before solving starts
- **Inprocessing:** During solving, periodically simplify

Modern solvers use both.

---

## Topic 6: Your Project - Honest Technical Discussion

### What Algorithm 3 Actually Does

**Input:** CNF formula F
**For each clause C:**
1. Try assigning negations of literals in C
2. Apply BCP on F without C
3. If conflict → entire clause C is redundant
4. If some literal ℓⱼ becomes false → can remove ℓⱼ

**Level:** Propositional logic (CNF clauses)
**Method:** BCP with negated literals
**Output:** Shortened/removed clauses

### What You Actually Did

**Input:** Logic-LLM constraint set
**For each constraint:**
1. Check if it matches redundancy pattern
2. Pattern 1: x==a exists, x!=b is redundant
3. Pattern 2: Exact duplicate
4. Mark for removal

**Level:** First-order/semantic constraints
**Method:** String pattern matching
**Output:** Removed constraints

### Key Differences

| Aspect | Algorithm 3 | Your Work |
|--------|-------------|-----------|
| **Input** | CNF clauses | Structured constraints |
| **Method** | BCP with ¬literals | Pattern matching |
| **Abstraction** | Propositional | First-order |
| **Detection** | Dynamic (BCP run) | Static (pattern check) |
| **Complexity** | Depends on BCP | O(n²) |
| **Generality** | Any redundancy BCP finds | Only specific patterns |

### Why This Happened
- Logic-LLM doesn't expose CNF level
- You worked at available abstraction level
- Adapted principle, not algorithm
- Should have titled differently

### What to Say
"My implementation adapts preprocessing principles to a different level. Algorithm 3's essence is removing redundancy before solving - I implemented this at Logic-LLM's constraint level rather than CNF level. The technique is simpler (pattern matching vs BCP) and less general, but achieves the same goal: reduce problem size while preserving correctness. I should have been clearer this was principle-inspired adaptation, not faithful Algorithm 3 implementation."

---

## Topic 7: Graph Coloring (Your Exercise 1)

### Problem
Given graph G = (V, E), can we color vertices with k colors such that no adjacent vertices share a color?

### SAT Encoding
**Variables:** x_{v,c} = "vertex v has color c"

**Constraints:**
1. **At least one color per vertex:**
   ```
   For each v: (x_{v,1} ∨ x_{v,2} ∨ ... ∨ x_{v,k})
   ```

2. **At most one color per vertex:**
   ```
   For each v, for all c₁ ≠ c₂: (¬x_{v,c₁} ∨ ¬x_{v,c₂})
   ```

3. **Adjacent vertices different colors:**
   ```
   For each edge (u,v), for each color c: (¬x_{u,c} ∨ ¬x_{v,c})
   ```

### Your Implementation
- Myciel3: Chromatic number 4 (3-colorable? NO, 4-colorable? YES)
- Queen5_5: Chromatic number 5
- Generated DIMACS CNF, verified with MiniSat

### Key Points
- Reduction from graph problem to SAT
- Polynomial-size encoding
- Practical approach: try k=1,2,3... until SAT

---

## Topic 8: N-Queens (Your Exercise 2)

### Problem
Place N queens on N×N board such that no two attack each other.

### SAT Encoding
**Variables:** x_{i,j} = "queen at position (i,j)"

**Constraints:**
1. **Exactly one queen per row:** For each row i:
   ```
   (x_{i,1} ∨ ... ∨ x_{i,N})  [at least one]
   (¬x_{i,j} ∨ ¬x_{i,k}) for all j≠k  [at most one]
   ```

2. **At most one per column:** For each column j:
   ```
   (¬x_{i,j} ∨ ¬x_{k,j}) for all i≠k
   ```

3. **At most one per diagonal:** For each diagonal:
   ```
   (¬x_{i,j} ∨ ¬x_{k,ℓ}) if on same diagonal
   ```

### Solution Counting
```python
count = 0
while solver.solve():
    count += 1
    solution = extract_current_solution()
    blocking_clause = [¬x for x in solution]
    solver.add_clause(blocking_clause)
return count
```

**Blocking prevents finding same solution twice**

### Your Results
- N=8: 92 solutions (verified against OEIS A000170)
- Incremental SAT solving
- PySAT with Glucose3 solver

---

## Topic 9: Complexity Theory

### P vs NP
- **P:** Problems solvable in polynomial time
- **NP:** Problems verifiable in polynomial time
- **NP-Complete:** Hardest problems in NP
- **NP-Hard:** At least as hard as NP-Complete

### SAT is NP-Complete
- **Cook-Levin Theorem (1971):** First NP-Complete problem
- Any NP problem reduces to SAT in polynomial time
- Fundamental in complexity theory

### Practical Performance
Despite NP-Completeness:
- Modern solvers handle millions of variables
- Industrial applications verify hardware/software
- Average-case much better than worst-case

### Why Solvers Work
- Structure in real-world instances
- CDCL learning prunes search space
- Good heuristics (VSIDS, phase saving)
- Preprocessing reduces problem size

---

## Topic 10: Modern SAT Solver Architecture

### Typical Pipeline
```
Input CNF
    ↓
[Preprocessing]
    ↓
[CDCL Loop]
    ├→ Variable selection (VSIDS)
    ├→ Unit propagation (BCP)
    ├→ Conflict analysis
    ├→ Clause learning
    ├→ Backjumping
    └→ Restart (periodic)
    ↓
[Inprocessing] (periodic)
    ↓
SAT/UNSAT + Model
```

### Key Components

**1. Variable Selection**
- **VSIDS (Variable State Independent Decaying Sum):**
  - Track variable activity in conflicts
  - Decay scores over time
  - Select high-activity variables

**2. Clause Database**
- Original clauses (permanent)
- Learned clauses (can delete)
- Clause deletion strategies (LBD, activity)

**3. Restarts**
- Escape bad search branches
- Luby sequence or geometric
- Keep learned clauses

**4. Phase Saving**
- Remember last polarity of variables
- Reuse on restart
- Exploits locality

### State-of-the-Art Solvers
- **CaDiCaL:** Modern, clean implementation
- **Kissat:** Competition winner
- **Glucose:** Learning rate-based branching
- **MiniSat:** Classic, educational

---

## Topic 11: Applications of SAT

### Hardware Verification
- **Equivalence checking:** Do two circuits compute same function?
- **Model checking:** Does system satisfy specification?
- **Bug finding:** Can property be violated?

### Software Verification
- **Symbolic execution:** Explore program paths
- **Test generation:** Find inputs covering branches
- **Bounded model checking:** Check properties for N steps

### Planning & Scheduling
- **AI Planning:** Find action sequence to goal
- **Resource allocation:** Schedule tasks with constraints
- **Configuration:** Valid system configurations

### Bioinformatics
- **Haplotype inference:** Genetic data analysis
- **Phylogeny:** Evolutionary tree construction

### Cryptanalysis
- Encode cipher as SAT
- Solution reveals key
- SHA-1 preimage attacks

---

## Topic 12: Proof Systems & Certificates

### Resolution
**Rule:** From (A ∨ x) and (B ∨ ¬x), derive (A ∨ B)

**Resolution Proof:**
- Sequence of resolution steps
- Derives empty clause (contradiction)
- Proves UNSAT

### DRAT (Deletion Resolution Asymmetric Tautology)
Modern proof format for UNSAT:
- Compact representation
- Can verify correctness
- Used in SAT competitions

### Certificates
- **SAT:** Model (assignment satisfying formula)
- **UNSAT:** Resolution proof or DRAT proof
- Allows independent verification

---

## Common Oral Exam Questions & Answers

### Q: What is SAT?
**A:** Boolean satisfiability problem - given a Boolean formula, does an assignment exist making it true? NP-complete, but practical solvers work well due to problem structure.

### Q: Explain DPLL vs CDCL
**A:** DPLL: systematic search with unit propagation and backtracking. CDCL: adds conflict learning and non-chronological backjumping. CDCL learns from mistakes, drastically faster on real instances.

### Q: What is BCP?
**A:** Boolean Constraint Propagation - iteratively derives forced assignments from unit clauses. Core of modern SAT solvers. O(1) amortized with watched literals.

### Q: Why preprocess?
**A:** Simplify formula before solving to reduce search space. Techniques include subsumption, variable elimination, vivification. Small preprocessing time can yield large solving speedup.

### Q: What is vivification?
**A:** Algorithm 3 - removes/shortens redundant clauses by applying BCP with negated literals. If BCP finds conflict, clause is redundant. Works on CNF level.

### Q: Explain your project honestly
**A:** I implemented constraint-level preprocessing inspired by vivification. Unlike Algorithm 3 which uses BCP on CNF, I used pattern matching on semantic constraints in Logic-LLM. Achieved 39.4% reduction with 100% correctness, but at a different abstraction level than classical vivification.

### Q: Graph coloring encoding?
**A:** Variables x_{v,c} for "vertex v has color c". Constraints: each vertex has exactly one color, adjacent vertices have different colors. Reduces graph problem to SAT.

### Q: N-Queens solution counting?
**A:** Incremental SAT: find solution, add blocking clause preventing that exact configuration, repeat until UNSAT. Count total solutions found.

### Q: Why is SAT NP-complete important?
**A:** First NP-complete problem (Cook-Levin). Any NP problem reduces to SAT, making SAT solvers universal problem-solving engines. Central to complexity theory.

### Q: How do modern solvers handle large instances?
**A:** CDCL learning, effective heuristics (VSIDS), preprocessing, inprocessing, restarts, watched literals. Real-world structure makes average case tractable despite worst-case hardness.

---

## Strategy for Meeting

### 1. Preparation
- Review this entire document
- Practice explaining concepts aloud
- Prepare to draw diagrams (implication graphs, search trees)
- Know your two projects cold

### 2. Honesty First
Start meeting with:
"I need to clarify my project. I called it vivification but it's actually constraint-level pattern matching inspired by vivification principles. Algorithm 3 operates on CNF with BCP; mine works on semantic constraints with pattern detection. I should have been more accurate in my presentation."

### 3. Show Understanding
Demonstrate you know:
- What real vivification is (Algorithm 3)
- How BCP works
- CNF vs semantic level differences
- Your actual contribution accurately

### 4. Answer Broadly
Be ready for questions on:
- SAT basics (definitions, NP-completeness)
- DPLL and CDCL algorithms
- BCP mechanics
- Preprocessing techniques
- Your two exercises
- Modern solver architecture

### 5. Stay Calm
- Admit what you don't know
- Don't guess or make up answers
- Say "I'm not sure, but I can reason about it..."
- Show thinking process, not just memorization

---

## Quick Reference: Key Formulas & Definitions

**CNF:** (ℓ₁ ∨ ℓ₂) ∧ (ℓ₃ ∨ ℓ₄) ∧ ...

**Unit Clause:** Single literal clause (ℓ)

**Resolution:** (A ∨ x) ∧ (B ∨ ¬x) ⊢ (A ∨ B)

**1-UIP:** First decision variable reachable from conflict in implication graph

**VSIDS:** Activity-based variable selection heuristic

**Watched Literals:** Efficient unit propagation (2 per clause)

**Subsumption:** C₁ ⊆ C₂ → remove C₂

**Variable Elimination:** Remove var by resolving all occurrences

**Vivification:** BCP(¬ℓ₁,...,¬ℓᵢ, F\C) to detect redundancy in C

---

## Final Advice

**Be honest.** Acknowledge the vivification issue immediately.

**Show knowledge.** Demonstrate understanding of course material.

**Stay composed.** Answer what you know, admit what you don't.

**Learn from it.** This experience teaches precision in technical claims.

You have real accomplishments (graph coloring, N-Queens, working preprocessing). The vivification framing was wrong, but the work has value. Own the mistake, show your knowledge, and you'll get through this.

Good luck!
