# Advanced Frame Properties for GL+I

## Introduction

This document establishes the advanced frame-theoretic properties of GL+I, providing rigorous characterizations of the dual accessibility relation structure and their semantic consequences. These results form the foundation for completeness and model construction techniques.

## Frame Class Characterization

### Definition: GL+I Frame Class

**Definition 4.1**: The class of GL+I frames is:
$$\mathcal{F}_{GL+I} = \{⟨W, R_□, R_I⟩ : W ≠ ∅ ∧ \text{GL-Cond}(R_□) ∧ \text{I-Cond}(R_I)\}$$

Where:
- **GL-Cond(R_□)**: R_□ is transitive, irreflexive, and conversely well-founded
- **I-Cond(R_I)**: R_I is transitive and R_□ ⊆ R_I

### Theorem 4.2: Frame Class Properties

**Theorem**: $\mathcal{F}_{GL+I}$ has the following properties:
1. **Closure under subframes**: If F ∈ $\mathcal{F}_{GL+I}$ and F' is a subframe of F, then F' ∈ $\mathcal{F}_{GL+I}$
2. **Closure under disjoint unions**: If F₁, F₂ ∈ $\mathcal{F}_{GL+I}$, then F₁ ⊔ F₂ ∈ $\mathcal{F}_{GL+I}$
3. **Finite model property**: Every satisfiable formula has a finite model in $\mathcal{F}_{GL+I}$

**Proof**:
1. **Subframes**: Let F = ⟨W, R_□, R_I⟩ ∈ $\mathcal{F}_{GL+I}$ and F' = ⟨W', R'_□, R'_I⟩ where W' ⊆ W, R'_□ = R_□ ∩ (W' × W'), R'_I = R_I ∩ (W' × W').
   - R'_□ inherits transitivity, irreflexivity, and well-foundedness from R_□
   - R'_I inherits transitivity from R_I
   - R'_□ ⊆ R'_I follows from R_□ ⊆ R_I
   
2. **Disjoint unions**: Let F₁ = ⟨W₁, R₁_□, R₁_I⟩, F₂ = ⟨W₂, R₂_□, R₂_I⟩ with W₁ ∩ W₂ = ∅.
   - F₁ ⊔ F₂ = ⟨W₁ ∪ W₂, R₁_□ ∪ R₂_□, R₁_I ∪ R₂_I⟩
   - Properties are preserved component-wise
   
3. **Finite model property**: By filtration (see Theorem 4.15) □

## Accessibility Relation Analysis

### Definition 4.3: Accessibility Degrees

For frame F = ⟨W, R_□, R_I⟩ and world w ∈ W:

**□-degree**: deg_□(w) = |{v ∈ W : wR_□v}|
**I-degree**: deg_I(w) = |{v ∈ W : wR_Iv}|
**Extension degree**: ext(w) = deg_I(w) - deg_□(w)

### Theorem 4.4: Degree Properties

**Theorem**: For any GL+I frame F and world w:
1. deg_□(w) ≤ deg_I(w) (by inclusion condition)
2. ext(w) ≥ 0 (non-negative extension)
3. ext(w) = 0 iff R_□(w) = R_I(w) (local collapse condition)

**Proof**: Immediate from definitions and R_□ ⊆ R_I □

### Definition 4.5: Frame Types

**Minimal Frame**: ext(w) = 0 for all w ∈ W (R_I = R_□)
**Proper Extension Frame**: ∃w ∈ W such that ext(w) > 0
**Uniform Extension Frame**: ext(w) = k for all w ∈ W, some constant k > 0

## Constraint Propagation

### Theorem 4.6: Transitivity Constraint Propagation

**Theorem**: In any GL+I frame, if wR_Iv and vR_Iu, then wR_Iu must hold.

**Proof**: Direct from transitivity of R_I. This constrains possible frame constructions.

**Corollary 4.7**: When adding edges to extend R_□ to R_I, transitivity closure must be computed.

### Algorithm 4.8: Valid Frame Extension

```
Algorithm: ExtendFrame(F_base, E_new)
Input: GL frame F_base = ⟨W, R_□⟩, edge set E_new
Output: GL+I frame F_extended or FAIL

1. Initialize R_I := R_□ ∪ E_new
2. Compute transitive closure: R_I := R_I*
3. Check if R_□ ⊆ R_I (should hold by construction)
4. Verify R_I is transitive (should hold by construction)
5. Return F_extended = ⟨W, R_□, R_I⟩
```

**Complexity**: O(|W|³) for transitive closure computation

## Frame Morphisms and Bisimulation

### Definition 4.9: GL+I Frame Morphism

A function f: W₁ → W₂ is a **GL+I morphism** between frames F₁, F₂ if:
1. **□-preservation**: wR¹_□v ⟹ f(w)R²_□f(v)
2. **I-preservation**: wR¹_Iv ⟹ f(w)R²_If(v)
3. **□-reflection**: f(w)R²_□f(v) ⟹ ∃u(wR¹_□u ∧ f(u) = f(v))
4. **I-reflection**: f(w)R²_If(v) ⟹ ∃u(wR¹_Iu ∧ f(u) = f(v))

### Theorem 4.10: Morphism Properties

**Theorem**: GL+I morphisms preserve and reflect satisfaction of all GL+I formulas.

**Proof**: By induction on formula structure, using standard modal logic techniques extended to dual accessibility. □

### Definition 4.11: GL+I Bisimulation

A relation Z ⊆ W₁ × W₂ is a **GL+I bisimulation** if for all (w,v) ∈ Z:
1. **Atomic harmony**: For all p ∈ Prop, w ∈ V₁(p) iff v ∈ V₂(p)
2. **□-forth**: If wR¹_□w', then ∃v' such that vR²_□v' and (w',v') ∈ Z
3. **□-back**: If vR²_□v', then ∃w' such that wR¹_□w' and (w',v') ∈ Z
4. **I-forth**: If wR¹_Iw', then ∃v' such that vR²_Iv' and (w',v') ∈ Z
5. **I-back**: If vR²_Iv', then ∃w' such that wR¹_Iw' and (w',v') ∈ Z

### Theorem 4.12: Bisimulation Invariance

**Theorem**: If w₁ and w₂ are GL+I bisimilar, then for any GL+I formula φ:
w₁ ⊨ φ iff w₂ ⊨ φ

**Proof**: Standard bisimulation argument extended to dual accessibility relations. □

## Model Construction Techniques

### Construction 4.13: Minimal Model Extensions

**Problem**: Given GL model M and formula φ such that M ⊭ φ, construct GL+I model M' such that M' ⊨ φ.

**Algorithm**:
1. **Identify failure points**: Find worlds where φ fails in M
2. **Add I-accessibility**: Extend R_I minimally to make φ true
3. **Compute closure**: Ensure transitivity of R_I
4. **Verify constraints**: Check R_□ ⊆ R_I maintained

**Example**: If φ = Ip ∧ ¬□p:
- Find world w where □p fails but we want Ip true
- Add R_I edges to worlds satisfying p
- Ensure no R_□ edges to worlds not satisfying p

### Construction 4.14: Canonical Model Preparation

**Canonical Frame Construction**:
- W^c = {Γ : Γ is maximal GL+I-consistent set}
- ΓR^c_□Δ iff {A : □A ∈ Γ} ⊆ Δ
- ΓR^c_IΔ iff {A : IA ∈ Γ} ⊆ Δ

**Key Properties**:
- R^c_□ ⊆ R^c_I (by axiom I3)
- Both relations are transitive
- Truth lemma: Γ ⊨ A iff A ∈ Γ

## Filtration Method

### Theorem 4.15: GL+I Filtration

**Theorem**: GL+I has the finite model property via filtration.

**Proof Sketch**:
1. **Setup**: Given satisfiable formula φ, let Sub(φ) be its subformulas
2. **Equivalence**: Define w ≡_φ v iff w and v satisfy same formulas in Sub(φ)
3. **Quotient construction**: Build filtered frame F_φ = ⟨W/≡_φ, R'_□, R'_I⟩
4. **Relation definition**:
   - [w]R'_□[v] iff ∃w' ∈ [w], v' ∈ [v] such that w'R_□v'
   - [w]R'_I[v] iff ∃w' ∈ [w], v' ∈ [v] such that w'R_Iv'
5. **Property preservation**: Verify frame conditions are maintained
6. **Satisfaction preservation**: Show φ remains satisfiable in F_φ

**Technical Challenge**: Ensuring R'_□ ⊆ R'_I in filtered model.

**Solution**: The inclusion is preserved because if [w]R'_□[v], then by definition there exist representatives with wR_□v, which by frame condition gives wR_Iv, which ensures [w]R'_I[v].

## Complexity Analysis

### Theorem 4.16: Model Checking Complexity

**Theorem**: Model checking for GL+I formulas is in PSPACE.

**Proof**: 
- Formula depth bounds recursive calls
- Each world visited at most once per subformula
- Space requirement: O(|φ| × |W|)
- Time requirement: O(|φ| × |W| × max(|R_□|, |R_I|))

### Theorem 4.17: Satisfiability Complexity

**Theorem**: Satisfiability for GL+I is PSPACE-complete.

**Proof Sketch**:
- **Upper bound**: Guess model of exponential size, verify in polynomial space
- **Lower bound**: Reduction from GL satisfiability (which is PSPACE-complete)

## Special Frame Classes

### Definition 4.18: Rooted Frames

A GL+I frame is **rooted** if there exists w₀ ∈ W such that for all v ∈ W, either v = w₀ or w₀R*_Iv (where R*_I is the reflexive-transitive closure).

### Definition 4.19: Tree Frames

A GL+I frame is a **tree** if:
1. It is rooted
2. For all w ∈ W, |{v : vR_Iv}| ≤ 1 (unique predecessor under R_I)
3. R_□ ⊆ R_I (standard inclusion)

### Theorem 4.20: Tree Frame Properties

**Theorem**: Tree frames form a complete subclass for GL+I.

**Proof**: Every GL+I formula satisfiable in some frame is satisfiable in a tree frame (by unraveling construction). □

## Frame Definability

### Theorem 4.21: Axiom-Frame Correspondence

**Complete Correspondence Table**:

| Axiom | Frame Property | First-Order Definition |
|-------|---------------|----------------------|
| I1 | R_I satisfies K | ∀w,v,u((wR_Iv ∧ vR_Iu) → ∃z(wR_Iz ∧ (∀A(z⊨A iff (v⊨A→u⊨A))))) |
| I2 | R_I is transitive | ∀w,v,u((wR_Iv ∧ vR_Iu) → wR_Iu) |
| I3 | R_□ ⊆ R_I | ∀w,v(wR_□v → wR_Iv) |

**Note**: The I1 correspondence is more complex due to the modal nature of distribution.

### Theorem 4.22: Van Benthem Characterization

**Theorem**: GL+I frame class is not first-order definable.

**Proof**: Similar to standard GL result - the conversely well-founded property cannot be expressed in first-order logic. □

## Summary

This advanced frame theory provides:

1. **Structural Characterization**: Complete description of GL+I frame classes
2. **Construction Methods**: Systematic techniques for building models
3. **Morphism Theory**: Tools for relating different frames
4. **Complexity Bounds**: Computational limits for reasoning
5. **Special Cases**: Important subclasses with nice properties

These results establish the semantic foundations necessary for completeness theory and provide practical tools for model construction and verification.

**Next**: Week 5 will develop canonical model theory and completeness preparation based on these frame-theoretic foundations.