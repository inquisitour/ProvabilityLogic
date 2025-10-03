# Frame Diagrams and Visual Representations

## Diagram Conventions

### Notation System
- **Solid arrows (→)**: R□ relations (provability accessibility)
- **Dashed arrows (⇢)**: Additional Rᵢ relations beyond R□
- **Double arrows (⟹)**: Relations present in both R□ and Rᵢ
- **World labels**: w₀, w₁, w₂, etc.
- **Proposition sets**: [p, q, r] indicating which propositions are true at each world
- **Boxed worlds**: □ Special emphasis for important worlds
- **Shaded regions**: Grouping of worlds with similar properties

## Basic Frame Structures

### Frame F₁: Minimal Non-Collapse

```
    w₀
   ╱ ╲
  ⟹   ⇢
 ╱     ╲
w₁     w₂
[p]    []
```

**Formal Specification**:
- W = {w₀, w₁, w₂}
- R□ = {(w₀, w₁)}
- Rᵢ = {(w₀, w₁), (w₀, w₂)}
- Inclusion: R□ ⊆ Rᵢ ✓

**Key Property**: Demonstrates w₀ ⊨ □p ∧ ¬Ip when V(p) = {w₁}

### Frame F₂: Transitivity Chain

```
w₀ ⟹ w₁ ⟹ w₂
 ╲             ╱
  ⇢-----------⇢
   (transitivity)
```

**Formal Specification**:
- W = {w₀, w₁, w₂}
- R□ = {(w₀, w₁), (w₁, w₂)}
- Rᵢ = {(w₀, w₁), (w₁, w₂), (w₀, w₂)}
- Transitivity: Both relations are transitive ✓

**Key Property**: Shows how Rᵢ transitivity is preserved and extends R□ transitivity

### Frame F₃: Complex Inclusion

```
      w₀
    ╱  |  ╲
   ⟹   ⟹   ⇢
  ╱    |    ╲
 w₁    w₂    w₃
 |⟹   |⇢   [q]
 |     |
 w₄    w₅
[p,r] [r]
```

**Formal Specification**:
- W = {w₀, w₁, w₂, w₃, w₄, w₅}
- R□ = {(w₀, w₁), (w₀, w₂), (w₁, w₄)}
- Rᵢ = R□ ∪ {(w₀, w₃), (w₂, w₅)}
- Multiple levels demonstrating inclusion preservation

## Specialized Frame Types

### Frame F₄: Irreflexive GL Base

```
   ┌─────────────┐
   │    GL       │
   │  Structure  │
   └─────────────┘
        w₀
       ╱  ╲
      ⟹    ⟹
     ╱      ╲
    w₁      w₂
    │⟹     
    │       
    w₃      
```

**Properties**:
- R□ is irreflexive: ∀w(¬wR□w)
- R□ is transitive: Chains preserved
- Rᵢ extends R□ while maintaining properties
- No self-loops in R□ (GL requirement)

### Frame F₅: Finite Chains

```
Level 0:    [w₀]
            ╱  ╲
Level 1:  [w₁] [w₂]
          ╱ ╲   │⇢
Level 2: [w₃][w₄][w₅]
```

**Properties**:
- Finite depth (3 levels)
- No infinite ascending chains
- Conversely well-founded
- All GL frame requirements satisfied

**Accessibility Matrix**:

|     | w₀ | w₁ | w₂ | w₃ | w₄ | w₅ |
|-----|----|----|----|----|----|----|
| **w₀** | 0  | □I | □I | 0  | 0  | I  |
| **w₁** | 0  | 0  | 0  | □I | □I | 0  |
| **w₂** | 0  | 0  | 0  | 0  | 0  | I  |
| **w₃** | 0  | 0  | 0  | 0  | 0  | 0  |
| **w₄** | 0  | 0  | 0  | 0  | 0  | 0  |
| **w₅** | 0  | 0  | 0  | 0  | 0  | 0  |

**Legend**: □ = R□ only, I = Rᵢ only, □I = both relations

## Frame Property Illustrations

### Property P₁: Inclusion R□ ⊆ Rᵢ

```
R□ Relations:      Rᵢ Relations:
w₀ → w₁           w₀ ⟹ w₁
w₀ → w₂           w₀ ⟹ w₂
                  w₀ ⇢ w₃
                  w₁ ⇢ w₄

Inclusion:        Every R□ arrow 
R□ ⊆ Rᵢ ✓        becomes Rᵢ arrow
```

### Property P₂: Transitivity Preservation

```
Original R□:          Extended Rᵢ:
w₀ → w₁ → w₂         w₀ ⟹ w₁ ⟹ w₂
                      ╲_____________╱
                            ⇢
                      (transitive closure)
```

### Property P₃: Non-Reflexivity

```
GL Requirement:       Our Extension:
   w₀                    w₀
   ╱│╲                  ╱│╲
  ╱ ✗ ╲               ⟹ ⇢ ⟹
 ╱ no  ╲             ╱   │  ╲
w₁  loop w₂         w₁   ?   w₂

R□ never loops       Rᵢ may have loops
```

## Model-Specific Diagrams

### Model M₁: Basic Non-Equivalence

```
Truth Assignment:
    w₀: []
   ╱    ╲
  ⟹      ⇢
 ╱        ╲
w₁: [p]   w₂: []

Evaluation:
□p: ∀v(w₀R□v → v⊨p) = p at w₁ ✓
Ip: ∀v(w₀Rᵢv → v⊨p) = p at w₁,w₂ ✗

Result: □p ∧ ¬Ip ✓
```

### Model M₂: Distribution Example

```
Truth Assignment:
    w₀: []
   ╱    ╲
  ⟹      ⇢
 ╱        ╲
w₁: [q]   w₂: [p,q]

Formula: p → q
w₁: ¬p ∨ q = ⊤ ∨ q = ⊤ ✓
w₂:  p ∨ q = ⊤ ∨ ⊤ = ⊤ ✓

I(p→q): All Rᵢ-worlds satisfy p→q ✓
```

### Model M₃: Axiom Verification

```
Axiom I1: I(A→B) → (IA→IB)
    w₀
   ╱  ╲
  ⟹    ⇢
 ╱      ╲
w₁      w₂
[A,B]   [¬A,B]

I(A→B): w₁⊨(A→B)✓, w₂⊨(A→B)✓ → I(A→B)✓
IA: w₁⊨A✓, w₂⊭A✗ → IA✗
IB: w₁⊨B✓, w₂⊨B✓ → IB✓
(IA→IB): ⊥→⊤ = ⊤ ✓

Axiom holds! ✓
```

## Comparative Frame Analysis

### Standard GL vs GL+I

```
Standard GL:          GL+I Extension:

    w₀                    w₀
   ╱  ╲                 ╱ │ ╲
  →    →               ⟹  ⇢  ⟹
 ╱      ╲             ╱   │   ╲
w₁      w₂           w₁   w₃   w₂

Single relation      Dual relations
R□ only             R□ ⊆ Rᵢ
```

### Expressive Power Comparison

```
GL Can Express:       GL+I Can Additionally Express:

□A: "A provable"      IA: "A aligned"
♢A: "A consistent"    ♦A: "A interface-consistent"
                      □A∧¬IA: "provable but not aligned"
                      IA∧¬□A: "aligned but not provable"

New Fixed Points:     B ↔ I(¬□B)
Traditional: B ↔ ¬□B  "B iff not-provably-not-B aligned"
```

## Construction Patterns

### Pattern C₁: Minimal Extension

```
Start:    w₀ → w₁
Add:      w₀ ⇢ w₂
Result:   w₀ ⟹ w₁
          w₀ ⇢ w₂

Properties:
- Minimal: Only one additional Rᵢ edge
- Non-collapse: Can show IA ≠ □A
- Simple: Easy to verify properties
```

### Pattern C₂: Transitive Extension

```
Start:    w₀ → w₁ → w₂
Add:      w₀ ⇢ w₂ (transitive closure)
Result:   w₀ ⟹ w₁ ⟹ w₂
           ╲_____________╱
                  ⇢

Properties:
- Preserves transitivity
- Extends chains naturally
- Maintains GL structure
```

### Pattern C₃: Layered Extension

```
Level-by-level construction:

Level 0: w₀
Level 1: w₁, w₂ (R□-accessible)
Level 2: w₃, w₄ (Rᵢ-accessible only)

      w₀
    ╱  │  ╲
   ⟹   ⟹   ⇢
  ╱    │    ╲
 w₁    w₂    w₃
      │⇢     │⇢
      │      │
      w₄     w₅

Properties:
- Layered structure
- Clear separation of relation types
- Systematic extension
```

## Frame Validation Diagrams

### Validation V₁: Inclusion Check

```
For each R□ edge, verify Rᵢ edge exists:

R□ edges:        Rᵢ verification:
w₀ → w₁    ⟹    w₀ ⟹ w₁ ✓
w₀ → w₂    ⟹    w₀ ⟹ w₂ ✓
w₁ → w₃    ⟹    w₁ ⟹ w₃ ✓

Inclusion R□ ⊆ Rᵢ verified ✓
```

### Validation V₂: Transitivity Check

```
For Rᵢ transitivity:
If wRᵢv and vRᵢu, then wRᵢu must hold

Chain: w₀ ⇢ w₁ ⇢ w₂
Check: w₀ ⇢ w₂ required
Status: w₀ ⇢ w₂ present ✓

Transitivity verified ✓
```

### Validation V₃: Well-Foundedness

```
Check for infinite ascending chains:

Path analysis:
w₃ → w₂ → w₁ → w₀ (finite) ✓
w₄ → w₁ → w₀ (finite) ✓
w₅ → w₂ → w₀ (finite) ✓

No infinite chains found ✓
Well-foundedness preserved ✓
```

## Summary Diagram

```
GL+I Frame Requirements Summary:

┌─────────────────────────────────┐
│        Frame F = ⟨W,R□,Rᵢ⟩      │
├─────────────────────────────────┤
│  R□ Properties (from GL):       │
│  • Transitive                   │
│  • Irreflexive                  │
│  • Conversely well-founded      │
│  • Finite chains                │
├─────────────────────────────────┤
│  Rᵢ Properties (new):           │
│  • Transitive                   │
│  • R□ ⊆ Rᵢ (inclusion)          │
│  • Extends accessibility        │
├─────────────────────────────────┤
│  Semantic Consequences:         │
│  • □A → IA (always)             │
│  • IA ↛ □A (generally)          │
│  • Enhanced expressivity        │
│  • Preserved decidability       │
└─────────────────────────────────┘
```

These diagrams provide visual intuition for the formal semantic framework and serve as quick references for understanding the structural properties of GL+I models.