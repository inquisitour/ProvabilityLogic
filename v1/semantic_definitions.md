# Semantic Definitions for GL+I

## Kripke Frame Definition

### Basic Frame Structure

**Definition 3.1**: A *GL+I frame* is a tuple ℱ = ⟨W, R□, Rᵢ⟩ where:
- W is a non-empty set of possible worlds
- R□ ⊆ W × W is the provability accessibility relation
- Rᵢ ⊆ W × W is the interface accessibility relation

### Frame Conditions

**Standard GL Conditions for R□**:
1. **Transitivity**: ∀w,v,u ∈ W(wR□v ∧ vR□u → wR□u)
2. **Irreflexivity**: ∀w ∈ W(¬wR□w)  
3. **Finite Chains**: No infinite ascending R□-chains
4. **Conversely Well-Founded**: Every subset S ⊆ W has an R□-maximal element

**Interface Conditions for Rᵢ**:
1. **Transitivity**: ∀w,v,u ∈ W(wRᵢv ∧ vRᵢu → wRᵢu)
2. **Inclusion**: R□ ⊆ Rᵢ

**Remark**: Rᵢ inherits finite chain properties from R□ through the inclusion condition.

### Frame Properties

**Theorem 3.2**: Frame property inheritance

Given R□ ⊆ Rᵢ and transitivity of both relations:
1. If R□ is conversely well-founded, then Rᵢ restricted to R□-reachable worlds is conversely well-founded
2. The finite model property is preserved
3. Irreflexivity of R□ does not imply irreflexivity of Rᵢ

## Kripke Model Definition

### Model Structure

**Definition 3.3**: A *GL+I model* is a tuple 𝒦 = ⟨ℱ, V⟩ where:
- ℱ = ⟨W, R□, Rᵢ⟩ is a GL+I frame
- V: Prop → 𝒫(W) is a valuation function

### Satisfaction Relation

**Definition 3.4**: The satisfaction relation ⊨ is defined inductively:

**Atomic Formulas**:
- w ⊨ p iff w ∈ V(p)

**Boolean Connectives**:
- w ⊨ ¬A iff w ⊭ A
- w ⊨ A ∧ B iff w ⊨ A and w ⊨ B  
- w ⊨ A ∨ B iff w ⊨ A or w ⊨ B
- w ⊨ A → B iff w ⊭ A or w ⊨ B
- w ⊨ A ↔ B iff (w ⊨ A iff w ⊨ B)

**Modal Operators**:
- w ⊨ □A iff ∀v ∈ W(wR□v → v ⊨ A)
- w ⊨ IA iff ∀v ∈ W(wRᵢv → v ⊨ A)

**Derived Operators**:
- w ⊨ ♢A iff ∃v ∈ W(wR□v ∧ v ⊨ A)
- w ⊨ ♦A iff ∃v ∈ W(wRᵢv ∧ v ⊨ A)

## Semantic Properties

### Truth Conditions Analysis

**Theorem 3.5**: Inclusion property verification

For any model 𝒦 and world w:
If w ⊨ □A, then w ⊨ IA

*Proof*:
1. Assume w ⊨ □A
2. By definition: ∀v(wR□v → v ⊨ A)  
3. Since R□ ⊆ Rᵢ: ∀v(wR□v → wRᵢv)
4. Therefore: ∀v(wRᵢv → v ⊨ A) [by steps 2,3]
5. By definition: w ⊨ IA □

### Non-Collapse Verification

**Theorem 3.6**: Semantic non-collapse

There exist models 𝒦 and worlds w such that w ⊨ IA but w ⊭ □A

*Construction*:
- W = {w, v₁, v₂}
- R□ = {(w, v₁)}  
- Rᵢ = {(w, v₁), (w, v₂)}
- V(p) = {v₁, v₂}

*Verification*:
- w ⊨ Ip since ∀v(wRᵢv → v ⊨ p) and both v₁, v₂ ⊨ p
- w ⊭ □p since ∃v₂(wRᵢv₂ ∧ v₂ ⊨ p) but ¬wR□v₂

## Model Classes

### Standard GL Models

**Definition 3.7**: A model is *GL-standard* if Rᵢ = R□

In GL-standard models: IA ↔ □A for all formulas A

### Proper Extensions  

**Definition 3.8**: A model is a *proper extension* if R□ ⊊ Rᵢ (strict inclusion)

**Theorem 3.9**: Existence of proper extensions

For any GL model ℳ = ⟨W, R□, V⟩, there exists a proper extension ℳ' = ⟨W, R□, Rᵢ, V⟩ with R□ ⊊ Rᵢ that satisfies all frame conditions.

### Canonical Models

**Definition 3.10**: The canonical model construction for GL+I

Given the set of maximal consistent sets Δ:
- W^c = {Δ : Δ is GL+I maximal consistent}
- ΔR□^c Γ iff {A : □A ∈ Δ} ⊆ Γ  
- ΔRᵢ^c Γ iff {A : IA ∈ Δ} ⊆ Γ
- V^c(p) = {Δ ∈ W^c : p ∈ Δ}

**Theorem 3.11**: Canonical model properties

The canonical model satisfies:
1. R□^c ⊆ Rᵢ^c (by axiom I3)
2. Both relations are transitive
3. Truth Lemma: Δ ⊨ A iff A ∈ Δ

## Correspondence Theory

### Frame-Formula Correspondences

**Theorem 3.12**: Axiom-frame correspondences

| Axiom | Frame Property | Correspondence |
|-------|---------------|----------------|
| I1 | Rᵢ satisfies K-property | ∀w,v,u(wRᵢv ∧ vRᵢu → wRᵢu) |
| I2 | Rᵢ is transitive | Same as above |
| I3 | R□ ⊆ Rᵢ | ∀w,v(wR□v → wRᵢv) |

### Additional Correspondences

**Theorem 3.13**: Extended correspondences

- **♦A → ♢A** corresponds to **R□ ⊆ Rᵢ**
- **□A ↔ □IA** corresponds to **R□ ⊆ Rᵢ ∧ ∀w,v(wRᵢv ∧ IA ∈ Γ(w) → A ∈ Γ(v))**

where Γ(w) = {A : w ⊨ A}.

## Finite Model Property

### Filtration Method

**Theorem 3.14**: Finite model property preservation

If formula φ is satisfiable in some GL+I model, then φ is satisfiable in a finite GL+I model.

*Proof Strategy*:
1. Start with satisfying model ℳ = ⟨W, R□, Rᵢ, V⟩
2. Define equivalence ≡_φ on W by: w ≡_φ v iff w and v satisfy the same subformulas of φ
3. Construct quotient model ℳ' = ⟨W', R□', Rᵢ', V'⟩
4. Verify that inclusion R□' ⊆ Rᵢ' is preserved
5. Show ℳ' ⊨ φ

### Complexity Analysis

**Theorem 3.15**: Model size bounds

Any satisfiable formula φ with n subformulas is satisfiable in a model with at most 2^n worlds.

*Proof*: Standard filtration argument adapted for dual accessibility relations.

## Semantic Equivalences

### Formula Equivalences

**Theorem 3.16**: Key semantic equivalences

In all GL+I models:
1. □A ↔ □IA
2. I□A ↔ □A  
3. ♦A → ♢A
4. ¬(IA ∧ ¬□A ∧ □¬A) (consistency constraint)

### Model Transformations

**Definition 3.17**: Model morphisms

A function f: W₁ → W₂ is a GL+I morphism between models ℳ₁, ℳ₂ if:
1. wR□v in ℳ₁ implies f(w)R□f(v) in ℳ₂
2. wRᵢv in ℳ₁ implies f(w)Rᵢf(v) in ℳ₂  
3. Valuation preservation: w ⊨ p in ℳ₁ iff f(w) ⊨ p in ℳ₂

**Theorem 3.18**: Morphism preservation

GL+I morphisms preserve satisfaction of all formulas.

## Completeness Preparation

### Semantic Consistency

**Definition 3.19**: A set Γ is *semantically consistent* if there exists a model ℳ and world w such that w ⊨ A for all A ∈ Γ.

**Theorem 3.20**: Semantic-syntactic consistency relationship

For any set Γ of GL+I formulas:
Γ is GL+I consistent iff Γ is semantically consistent

*Note*: Full proof requires completeness theorem (future work).

### Model Existence  

**Theorem 3.21**: Model existence theorem

Every GL+I consistent set of formulas is satisfiable in some GL+I model.

*Proof Strategy*: Canonical model construction with proper handling of dual accessibility relations.

## Summary

The semantic framework for GL+I extends standard GL semantics with:
1. Dual accessibility relations satisfying R□ ⊆ Rᵢ
2. Preservation of all GL semantic properties
3. Additional expressive power through the interface operator
4. Maintained finite model property and decidability prospects

This provides the foundation for soundness proofs and expressive power analysis in subsequent development phases.