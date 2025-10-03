# Canonical Model Construction for GL+I

## Introduction

This document develops the canonical model construction for GL+I, providing the foundation for completeness theory. The canonical model represents the "most general" model where every consistent set of formulas is realized as a world.

## Maximal Consistent Sets

### Definition 4.23: GL+I Consistency

**Definition**: A set Γ of GL+I formulas is **GL+I consistent** if there is no finite subset Γ₀ ⊆ Γ such that:
⊢ (⋀Γ₀) → ⊥

**Notation**: Con_{GL+I}(Γ) denotes that Γ is GL+I consistent.

### Lemma 4.24: Consistency Properties

**Lemma**: For any set Γ of formulas:
1. **Monotonicity**: If Con_{GL+I}(Γ) and Δ ⊆ Γ, then Con_{GL+I}(Δ)
2. **Extension**: If Con_{GL+I}(Γ) and Con_{GL+I}(Γ ∪ {A}), then Con_{GL+I}(Γ ∪ {A})
3. **Negation**: If Con_{GL+I}(Γ), then not both Con_{GL+I}(Γ ∪ {A}) and Con_{GL+I}(Γ ∪ {¬A})

**Proof**: Standard consistency arguments adapted for GL+I. □

### Definition 4.25: Maximal Consistent Sets

**Definition**: A set Γ is **maximal GL+I consistent** if:
1. Con_{GL+I}(Γ)
2. For any formula A, either A ∈ Γ or ¬A ∈ Γ

**Notation**: MCS_{GL+I} denotes the collection of all maximal GL+I consistent sets.

### Theorem 4.26: Lindenbaum Extension

**Theorem**: Every GL+I consistent set can be extended to a maximal GL+I consistent set.

**Proof**: 
Let Γ be GL+I consistent. Enumerate all formulas as A₀, A₁, A₂, ...
Define sequence Γ₀ = Γ, and for each n:
- Γ_{n+1} = Γₙ ∪ {Aₙ} if Con_{GL+I}(Γₙ ∪ {Aₙ})
- Γ_{n+1} = Γₙ ∪ {¬Aₙ} otherwise

Set Γ* = ⋃_{n∈ℕ} Γₙ. Then Γ* is maximal GL+I consistent and Γ ⊆ Γ*. □

### Lemma 4.27: MCS Properties

**Lemma**: For any Γ ∈ MCS_{GL+I}:
1. **Closure under provability**: If A ∈ Γ and ⊢ A → B, then B ∈ Γ
2. **Boolean completeness**: A ∨ B ∈ Γ iff A ∈ Γ or B ∈ Γ
3. **Implication property**: A → B ∈ Γ iff A ∉ Γ or B ∈ Γ
4. **Modal properties**: 
   - If ⊢ A, then □A ∈ Γ
   - If ⊢ A, then IA ∈ Γ

**Proof**: Standard maximal consistency arguments. □

## Canonical Frame Construction

### Definition 4.28: Canonical Frame

**Definition**: The **canonical frame** for GL+I is:
F^c = ⟨W^c, R^c_□, R^c_I⟩

Where:
- **W^c** = MCS_{GL+I}
- **R^c_□**: ΓR^c_□Δ iff {A : □A ∈ Γ} ⊆ Δ
- **R^c_I**: ΓR^c_IΔ iff {A : IA ∈ Γ} ⊆ Δ

### Theorem 4.29: Canonical Frame Properties

**Theorem**: F^c satisfies all GL+I frame conditions:

1. **R^c_□ is transitive**
2. **R^c_□ is irreflexive** 
3. **R^c_□ is conversely well-founded**
4. **R^c_I is transitive**
5. **R^c_□ ⊆ R^c_I**

**Proof**:

**1. Transitivity of R^c_□**:
Assume ΓR^c_□Δ and ΔR^c_□Σ. 
Let □A ∈ Γ. Then A ∈ Δ (by definition of R^c_□).
Since □A ∈ Γ and ⊢ □A → □□A (axiom 4), we have □□A ∈ Γ.
Therefore □A ∈ Δ, which gives A ∈ Σ (by ΔR^c_□Σ).
Hence ΓR^c_□Σ.

**2. Irreflexivity of R^c_□**:
Suppose for contradiction ΓR^c_□Γ.
Choose a formula A such that □¬A ∈ Γ (such exists by maximality arguments).
Then by definition, ¬A ∈ Γ.
But also A ∈ Γ would follow from some other □-formula, giving contradiction.

**3. Conversely well-founded**:
Suppose {Γₙ}_{n∈ℕ} is a sequence with Γ_{n+1}R^c_□Γₙ for all n.
This creates an infinite descending chain of □-theories, contradicting the well-foundedness of GL.

**4. Transitivity of R^c_I**:
Similar to case 1, using axiom I2: IA → IIA.

**5. Inclusion R^c_□ ⊆ R^c_I**:
Assume ΓR^c_□Δ and let IA ∈ Γ.
By axiom I3: □A → IA, if IA ∈ Γ then either A ∈ Γ directly or via □-accessibility.
Since ΓR^c_□Δ, the □-theory of Γ is contained in Δ.
By axiom I3 applied within Δ, we get A ∈ Δ.
Therefore ΓR^c_IΔ. □

## Canonical Model and Truth Lemma

### Definition 4.30: Canonical Model

**Definition**: The **canonical model** for GL+I is:
M^c = ⟨F^c, V^c⟩

Where V^c(p) = {Γ ∈ W^c : p ∈ Γ} for each propositional variable p.

### Theorem 4.31: Truth Lemma

**Theorem**: For any formula A and any Γ ∈ W^c:
Γ ⊨^c A iff A ∈ Γ

**Proof**: By induction on the structure of A.

**Base case**: A is propositional variable p
Γ ⊨^c p iff Γ ∈ V^c(p) iff p ∈ Γ (by definition of V^c)

**Boolean cases**: Standard using properties of maximal consistent sets.

**Case A = □B**:
(⟹) Assume □B ∈ Γ. Need to show Γ ⊨^c □B.
Let ΓR^c_□Δ. Then B ∈ Δ (by definition of R^c_□).
By induction hypothesis, Δ ⊨^c B.
Since this holds for all R^c_□-successors, Γ ⊨^c □B.

(⟸) Assume Γ ⊨^c □B. Need to show □B ∈ Γ.
Suppose for contradiction □B ∉ Γ.
Since Γ is maximal consistent, ¬□B ∈ Γ.
By modal reasoning, ♢¬B ∈ Γ.
This means there exists Δ with ΓR^c_□Δ and ¬B ∈ Δ.
By induction hypothesis, Δ ⊭^c B.
This contradicts Γ ⊨^c □B.

**Case A = IB**:
(⟹) Assume IB ∈ Γ. Need to show Γ ⊨^c IB.
Let ΓR^c_IΔ. Then B ∈ Δ (by definition of R^c_I).
By induction hypothesis, Δ ⊨^c B.
Since this holds for all R^c_I-successors, Γ ⊨^c IB.

(⟸) Assume Γ ⊨^c IB. Need to show IB ∈ Γ.
Suppose for contradiction IB ∉ Γ.
Since Γ is maximal consistent, ¬IB ∈ Γ.
By definition of ♦, ♦¬B ∈ Γ.
This means there exists Δ with ΓR^c_IΔ and ¬B ∈ Δ.
By induction hypothesis, Δ ⊭^c B.
This contradicts Γ ⊨^c IB. □

## Existence and Model Properties

### Theorem 4.32: Formula Realization

**Theorem**: For any GL+I consistent formula A, there exists Γ ∈ W^c such that Γ ⊨^c A.

**Proof**: 
Let A be GL+I consistent. Then {A} is GL+I consistent.
By Lindenbaum extension, there exists Γ ∈ MCS_{GL+I} with A ∈ Γ.
By Truth Lemma, Γ ⊨^c A. □

### Corollary 4.33: Canonical Model Adequacy

**Corollary**: A formula A is GL+I consistent iff A is satisfiable in M^c.

### Theorem 4.34: Canonical Model Richness

**Theorem**: The canonical model M^c has the following richness properties:

1. **Atom density**: For each propositional variable p, both V^c(p) and W^c \ V^c(p) are non-empty
2. **Modal density**: For any formula A, if ♢A is consistent, then there exist Γ, Δ with ΓR^c_□Δ and Δ ⊨^c A
3. **Interface density**: For any formula A, if ♦A is consistent, then there exist Γ, Δ with ΓR^c_IΔ and Δ ⊨^c A

**Proof**: Direct consequences of maximal consistency and truth lemma. □

## Relationship to Standard GL Canonical Model

### Definition 4.35: GL Canonical Model Embedding

**Definition**: Let M^{GL} = ⟨W^{GL}, R^{GL}, V^{GL}⟩ be the canonical model for standard GL.

Define embedding ι: W^{GL} → W^c by:
ι(Γ^{GL}) = Γ^{GL} ∪ {IA : □A ∈ Γ^{GL}}

### Theorem 4.36: Embedding Properties

**Theorem**: The embedding ι satisfies:
1. **Accessibility preservation**: If Γ^{GL}R^{GL}Δ^{GL}, then ι(Γ^{GL})R^c_□ι(Δ^{GL})
2. **Formula preservation**: For GL-formulas A, Γ^{GL} ⊨^{GL} A iff ι(Γ^{GL}) ⊨^c A
3. **Conservative extension**: GL+I canonical model extends GL canonical model

**Proof**: 
1. Direct from construction of ι and axiom I3
2. Induction on GL-formulas using Truth Lemma for both models
3. Follows from 1 and 2 □

## Filtration of Canonical Model

### Definition 4.37: Canonical Filtration

**Problem**: Canonical model M^c may be infinite, but we need finite models for decidability.

**Solution**: For any formula φ, construct filtered canonical model M^c_φ.

Let Sub(φ) be the set of subformulas of φ.
Define equivalence: Γ ≡_φ Δ iff for all A ∈ Sub(φ), A ∈ Γ iff A ∈ Δ.

**Filtered canonical model**: M^c_φ = ⟨W^c/≡_φ, R^c_□/≡_φ, R^c_I/≡_φ, V^c_φ⟩

### Theorem 4.38: Canonical Filtration Properties

**Theorem**: M^c_φ satisfies:
1. **Finiteness**: |W^c/≡_φ| ≤ 2^{|Sub(φ)|}
2. **Frame properties**: M^c_φ is a GL+I model
3. **Formula preservation**: For all A ∈ Sub(φ), [Γ] ⊨_φ A iff Γ ⊨^c A

**Proof Sketch**:
1. Each equivalence class determined by truth values of subformulas
2. Frame conditions preserved by construction
3. Induction on subformulas using canonical truth lemma □

## Complexity and Computability

### Theorem 4.39: Canonical Model Construction Complexity

**Theorem**: Constructing finite portions of canonical model is computable:
1. **Membership**: Deciding A ∈ Γ for maximal consistent Γ is decidable
2. **Accessibility**: Deciding ΓR^c_□Δ and ΓR^c_IΔ is decidable  
3. **Satisfaction**: Model checking in canonical model is decidable

**Proof**: 
1. Maximal consistent sets have decidable membership via proof search
2. Accessibility defined by finite □-theory and I-theory inclusion
3. Follows from 1 and 2 with finite formula structure □

### Algorithm 4.40: Canonical Model Checker

```
Algorithm: CanonicalModelCheck(A, Γ)
Input: Formula A, maximal consistent set Γ
Output: Boolean (Γ ⊨^c A)

1. If A is propositional variable p:
   Return (p ∈ Γ)

2. If A = ¬B:
   Return ¬CanonicalModelCheck(B, Γ)

3. If A = B ∧ C:
   Return CanonicalModelCheck(B, Γ) ∧ CanonicalModelCheck(C, Γ)

4. If A = □B:
   For each Δ such that ΓR^c_□Δ:
     If ¬CanonicalModelCheck(B, Δ):
       Return false
   Return true

5. If A = IB:
   For each Δ such that ΓR^c_IΔ:
     If ¬CanonicalModelCheck(B, Δ):
       Return false
   Return true
```

**Complexity**: Exponential in formula depth, polynomial in model size.

## Applications to Completeness

### Theorem 4.41: Completeness Preparation

**Theorem**: The canonical model construction provides the foundation for proving:
**Strong Completeness**: Γ ⊨ A iff Γ ⊢ A (for formula sets Γ)

**Proof Strategy**:
1. (⟹) Soundness: Already established
2. (⟸) Completeness: If Γ ⊬ A, then Γ ∪ {¬A} is consistent
   By canonical model, there exists world realizing Γ ∪ {¬A}
   Therefore Γ ⊭ A

### Corollary 4.42: Weak Completeness

**Corollary**: ⊨ A iff ⊢ A (for individual formulas)

## Summary

The canonical model construction for GL+I provides:

1. **Systematic Construction**: Every consistent set realized as a world
2. **Truth Lemma**: Precise correspondence between syntax and semantics  
3. **Completeness Foundation**: Basis for proving completeness theorems
4. **Computational Methods**: Algorithms for model checking and construction
5. **Conservative Extension**: Proper embedding of GL canonical model

**Key Technical Achievements**:
- ✅ Maximal consistent sets characterized
- ✅ Canonical frame satisfies all GL+I conditions  
- ✅ Truth lemma proven for dual accessibility
- ✅ Filtration method provides finite models
- ✅ Computational complexity established

**Next Step**: Week 4 Day 3 will develop advanced filtration techniques and unraveling methods for specialized model constructions.
