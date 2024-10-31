# II. Preliminary Definitions and Framework

## A. Language (L)

### Definition 1 (Formal Language)
Let L be a first-order language containing:

1. Arithmetic Symbols
   - Constant: 0
   - Function symbols:
     * S (successor function)
     * + (addition)
     * × (multiplication)
   - Relation symbol: = (equality)

2. Logical Symbols
   - Connectives:
     * ¬ (negation)
     * ∧ (conjunction)
     * ∨ (disjunction)
     * → (implication)
     * ↔ (equivalence)
   - Quantifiers:
     * ∀ (universal)
     * ∃ (existential)

3. Modal Operators
   - □ (provability operator)
   - I (interface operator)

4. Variables and Syntax
   - Denumerable set of variables: x, y, z, ...
   - Parentheses: (, )
   - Additional syntax markers as needed

## B. Terms

### Definition 2 (Terms)
The set of terms T is the smallest set such that:

1. Basic Terms
   - 0 ∈ T
   - Any variable is in T

2. Compound Terms
   - If t ∈ T, then S(t) ∈ T
   - If t₁, t₂ ∈ T, then:
     * (t₁ + t₂) ∈ T
     * (t₁ × t₂) ∈ T

3. No other expressions are terms

## C. Formulas

### Definition 3 (Formulas)
The set of formulas F is the smallest set such that:

1. Atomic Formulas
   - If t₁, t₂ are terms, then t₁ = t₂ ∈ F

2. Modal Formulas
   - If A ∈ F, then:
     * ¬A ∈ F
     * □A ∈ F
     * I(A) ∈ F

3. Compound Formulas
   - If A, B ∈ F, then:
     * (A ∧ B) ∈ F
     * (A ∨ B) ∈ F
     * (A → B) ∈ F
     * (A ↔ B) ∈ F

4. Quantified Formulas
   - If A ∈ F and x is a variable, then:
     * ∀xA ∈ F
     * ∃xA ∈ F

## D. Basic Semantic Concepts

### Definition 4 (Substitution)
For a term t, variable x, and formula A:
- A[t/x] denotes the result of substituting t for all free occurrences of x in A
- A term t is free for x in A if no free occurrence of x in A occurs within the scope of a quantifier that binds a variable occurring in t

### Definition 5 (Scope)
1. For connectives: The scope is the entire formula formed
2. For quantifiers: The scope is the entire formula following the quantifier
3. For modal operators: The scope is the entire formula to which they are applied

### Notes
1. We follow standard conventions for omitting parentheses when no ambiguity arises
2. Free and bound variables are defined as usual
3. We assume standard definitions of subformulas and proper subformulas
4. All formulas are assumed to be well-formed according to the above rules
