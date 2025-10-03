# Notation Standards for GL+I

## Universal Notation Conventions

This document establishes standardized notation across all GL+I documentation to ensure consistency and clarity in mathematical exposition.

## Logical Symbols

### Basic Logical Connectives
- **Negation**: ¬A
- **Conjunction**: A ∧ B  
- **Disjunction**: A ∨ B
- **Implication**: A → B
- **Biconditional**: A ↔ B
- **Truth**: ⊤ (or sometimes omitted in tautologies)
- **Falsity**: ⊥

### Quantifiers
- **Universal**: ∀x, ∀v, ∀w (with appropriate variable binding)
- **Existential**: ∃x, ∃v, ∃w

### Modal Operators
- **Provability**: □A (box A)
- **Interface**: IA (I A, no space in formal contexts)
- **Standard Consistency**: ♢A := ¬□¬A (diamond A)
- **Interface Consistency**: ♦A := ¬I¬A (lozenge A)

## Provability and Semantic Relations

### Syntactic Relations
- **Provability in GL+I**: ⊢ A
- **Provability in standard GL**: ⊢_{GL} A  
- **Provability in PA**: ⊢_{PA} A
- **Non-provability**: ⊬ A

### Semantic Relations
- **Satisfaction**: w ⊨ A (world w satisfies formula A)
- **Model satisfaction**: M ⊨ A (formula A true in all worlds of model M)
- **Non-satisfaction**: w ⊭ A
- **Semantic entailment**: Γ ⊨ A (A follows semantically from set Γ)

### Equivalence Relations
- **Logical equivalence**: A ≡ B (same truth conditions)
- **Provable equivalence**: ⊢ A ↔ B
- **Semantic equivalence**: A ⊨⊩ B (mutual semantic entailment)

## Frame and Model Notation

### Frames
- **GL+I Frame**: ℱ = ⟨W, R□, R_I⟩
- **Standard GL Frame**: ℱ_{GL} = ⟨W, R□⟩
- **World Set**: W (always non-empty)
- **Provability Relation**: R□ ⊆ W × W
- **Interface Relation**: R_I ⊆ W × W

### Models
- **GL+I Model**: M = ⟨ℱ, V⟩ = ⟨W, R□, R_I, V⟩
- **Valuation Function**: V: Prop → 𝒫(W)
- **Truth Set**: V(p) ⊆ W (worlds where proposition p is true)

### Accessibility Notation
- **R□-accessibility**: wR□v (w R-box v)
- **R_I-accessibility**: wR_Iv (w R-I v)
- **Successor Sets**: 
  - R□(w) := {v ∈ W : wR□v}
  - R_I(w) := {v ∈ W : wR_Iv}

## Variable Conventions

### World Variables
- **Generic worlds**: w, v, u (in that order)
- **Specific worlds**: w₀, w₁, w₂, ... (with subscripts)
- **Distinguished world**: w* (when emphasizing a particular world)

### Formula Variables  
- **Generic formulas**: A, B, C (arbitrary formulas)
- **Propositions**: p, q, r, s (propositional variables)
- **Specific formulas**: φ, ψ, χ (phi, psi, chi for particular constructions)
- **Schema variables**: X, Y, Z (for formula schemas in axioms)

### Set Variables
- **Formula sets**: Γ, Δ, Σ (Gamma, Delta, Sigma)
- **World sets**: W, W', W₁, W₂
- **Proof sets**: Φ, Ψ (when discussing proof collections)

## Arithmetical Notation

### Gödel Numbering
- **Gödel number**: ⌜A⌝ (corner quotes for formula A)
- **Numeral**: n̄ (numeral representing number n)
- **Code function**: ⌜·⌝: Form → ℕ

### Provability Predicates
- **Standard provability**: Prf(x, y) (x is proof of y)
- **Interface provability**: Prf_I(x, y) (x is interface-proof of y)
- **Provability in T**: Prov_T(x) := ∃y Prf_T(y, x)

### Complexity Classes
- **Σ₁ formulas**: Existential arithmetic formulas
- **Π₁ formulas**: Universal arithmetic formulas  
- **Δ₁ formulas**: Both Σ₁ and Π₁

## Set Theory Notation

### Basic Set Operations
- **Membership**: x ∈ S
- **Subset**: A ⊆ B (includes equality)
- **Proper subset**: A ⊊ B (excludes equality)
- **Power set**: 𝒫(S) (all subsets of S)
- **Cartesian product**: A × B

### Special Sets
- **Natural numbers**: ℕ = {0, 1, 2, ...}
- **Integers**: ℤ
- **Empty set**: ∅
- **Propositional variables**: Prop
- **Formulas**: Form

## Proof Theory Notation

### Inference Rules
- **Horizontal line notation**:
  ```
  A, A → B
  --------  (MP)
      B
  ```

- **Premise/Conclusion format**:
  - From ⊢ A and ⊢ A → B, infer ⊢ B

### Derivation Notation
- **Derivation**: D: Γ ⊢ A (derivation D proves A from assumptions Γ)
- **Empty context**: ⊢ A (A is a theorem)
- **Assumption discharge**: [A]¹...B (assumption A with label 1 discharged)

## Semantic Definitions

### Satisfaction Clauses
- **Atomic**: w ⊨ p iff w ∈ V(p)
- **Negation**: w ⊨ ¬A iff w ⊭ A
- **Conjunction**: w ⊨ A ∧ B iff w ⊨ A and w ⊨ B
- **Implication**: w ⊨ A → B iff w ⊭ A or w ⊨ B
- **Box**: w ⊨ □A iff ∀v(wR□v → v ⊨ A)
- **Interface**: w ⊨ IA iff ∀v(wR_Iv → v ⊨ A)

## Special Notation for GL+I

### Axiom References
- **I1**: Distribution axiom for I
- **I2**: Self-reflection axiom for I  
- **I3**: Inclusion axiom (□A → IA)
- **GL**: Standard Löb axiom
- **K**: Distribution axiom for □
- **4**: Transitivity axiom for □

### Frame Conditions
- **Inclusion**: R□ ⊆ R_I
- **Transitivity**: ∀w,v,u(wRv ∧ vRu → wRu) [for both relations]
- **Irreflexivity**: ∀w(¬wRw) [for R□ only]
- **Well-foundedness**: No infinite ascending R□-chains

### Derived Operators
- **Standard consistency**: ♢A := ¬□¬A
- **Interface consistency**: ♦A := ¬I¬A
- **Iterated interface**: I^n A (n applications of I)
- **Mixed formulas**: Formulas containing both □ and I

## Typography Conventions

### Emphasis and Structure
- **Definitions**: Use **bold** for defined terms
- **Theorems**: Use *italics* for theorem statements
- **Examples**: Use `code formatting` for specific instances
- **Important results**: Use ***bold italics*** for crucial statements

### Mathematical Expressions
- **Inline formulas**: Use single $ delimiters
- **Display formulas**: Use double $$ delimiters  
- **Long derivations**: Use align environments
- **Truth tables**: Use standard table formatting

### Cross-References
- **Theorem references**: Theorem 2.3, Lemma 4.1
- **Definition references**: Definition 1.2
- **Section references**: Section 3.2
- **File references**: `filename.md`

## Consistency Checks

### Common Notation Errors to Avoid
- ❌ Mixing ⊢ and ⊨ (syntactic vs semantic)
- ❌ Using R_I vs Rᵢ inconsistently
- ❌ Confusing ♢ and ♦ (different consistency operators)
- ❌ Inconsistent variable scoping in quantifiers
- ❌ Missing parentheses in complex formulas

### Verification Checklist
- ✅ All modal operators clearly distinguished
- ✅ Accessibility relations consistently named
- ✅ Provability vs satisfaction clearly marked
- ✅ Variable binding explicitly indicated
- ✅ Frame vs model notation properly used

## Standard Abbreviations

### Frequently Used Terms
- **GL**: Gödel-Löb (logic)
- **GL+I**: Gödel-Löb with Interface operator
- **PA**: Peano Arithmetic
- **MP**: Modus Ponens
- **Nec□**: Necessitation for □
- **NecI**: Necessitation for I
- **iff**: if and only if
- **w.r.t.**: with respect to
- **s.t.**: such that

### Model-Theoretic Abbreviations
- **FMP**: Finite Model Property
- **CWF**: Conversely Well-Founded
- **Sat**: Satisfiable
- **Val**: Valid
- **Cons**: Consistent

## Documentation Standards

### File Organization
- **01-**: Foundational definitions
- **02-**: Technical development  
- **03-**: Advanced results
- **04-**: Applications and examples

### Section Numbering
- **Major sections**: 1, 2, 3, ...
- **Subsections**: 1.1, 1.2, 1.3, ...
- **Sub-subsections**: 1.1.1, 1.1.2, ...

### Reference Format
- **Theorems**: "Theorem X.Y" where X is section, Y is number
- **Definitions**: "Definition X.Y"  
- **Examples**: "Example X.Y"
- **Models**: "Model M_X" or "M₁, M₂, ..."

This notation standard ensures consistency across all GL+I documentation and facilitates clear mathematical communication.