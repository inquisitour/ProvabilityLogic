# Inference Rules for GL+I

## Standard Inference Rules

### Propositional Logic Rules

**Modus Ponens (MP)**:
```
A, A → B
---------  
    B
```

**Formal Statement**: If ⊢ A and ⊢ A → B, then ⊢ B

**Transitivity of Implication**:
```
A → B, B → C
------------
   A → C
```

**Hypothetical Syllogism**: Derivable from MP and propositional logic.

### Modal Logic Rules for □

**Necessitation for □ (Nec□)**:
```
A
---
□A
```

**Formal Statement**: If ⊢ A, then ⊢ □A

**Note**: This rule only applies to theorems, not to assumptions in derivations.

**Derived Rule - Modal Modus Ponens for □**:
```
□(A → B), □A
------------
    □B
```

*Derivation*:
1. □(A → B) (premise)
2. □A (premise)  
3. □(A → B) → (□A → □B) (axiom K)
4. □A → □B (MP, 1, 3)
5. □B (MP, 2, 4)

### Modal Logic Rules for I

**Necessitation for I (NecI)**:
```
A
---
IA
```

**Formal Statement**: If ⊢ A, then ⊢ IA

**Derived Rule - Modal Modus Ponens for I**:
```
I(A → B), IA
-----------
    IB
```

*Derivation*:
1. I(A → B) (premise)
2. IA (premise)
3. I(A → B) → (IA → IB) (axiom I1)  
4. IA → IB (MP, 1, 3)
5. IB (MP, 2, 4)

## Interaction Rules

### Cross-Modal Rules

**Inclusion Rule (derived from I3)**:
```
□A
---
IA
```

*Justification*: Direct application of axiom I3 with MP.

**Necessitation Transfer**:
```
□A
----
□IA
```

*Derivation*:
1. □A (premise)
2. □A → IA (axiom I3)
3. IA (MP, 1, 2)
4. □IA (Nec□, 3)

### Equivalent Transformations

**Double Necessitation Equivalence**:
```
□A ⊣⊢ □IA
```

*Left-to-Right*:
1. □A (assumption)
2. □A → IA (axiom I3)
3. IA (MP, 1, 2)  
4. □IA (Nec□, 3)

*Right-to-Left*: Requires semantic argument using frame properties.

## Derived Inference Rules

### Monotonicity Rules

**Monotonicity for □**:
```
A → B
------
□A → □B
```

*Derivation*:
1. A → B (premise)
2. □(A → B) (Nec□, 1)
3. □(A → B) → (□A → □B) (axiom K)
4. □A → □B (MP, 2, 3)

**Monotonicity for I**:
```
A → B  
------
IA → IB
```

*Derivation*:
1. A → B (premise)
2. I(A → B) (NecI, 1)
3. I(A → B) → (IA → IB) (axiom I1)
4. IA → IB (MP, 2, 3)

### Contraposition Rules

**Contraposition for □**:
```
□A → □B
-------
□¬B → □¬A
```

*Derivation*: Standard contraposition combined with properties of necessity.

**Contraposition for I**:
```
IA → IB
-------
I¬B → I¬A
```

*Derivation*: Similar to □ case using I-axioms.

## Consistency and Possibility Rules

### Standard Consistency Rules

**Consistency Introduction for □**:
```
¬□¬A
-----
♢A
```

**Consistency Elimination for □**:
```
♢A, □(A → B)
-----------
    ♢B
```

### Interface Consistency Rules

**Consistency Introduction for I**:
```
¬I¬A
-----
♦A
```

**Consistency Elimination for I**:
```
♦A, I(A → B)
-----------
    ♦B
```

**Consistency Relationship**:
```
♦A
---
♢A
```

*Derivation*:
1. ♦A (premise)
2. ¬I¬A (definition of ♦)
3. Suppose □¬A
4. □¬A → I¬A (axiom I3)
5. I¬A (MP, 3, 4)
6. Contradiction with step 2
7. ¬□¬A
8. ♢A (definition of ♢)

## Advanced Derivation Techniques

### Fixed Point Construction Rules

**Diagonalization for □** (Löb's Rule):
```
□(□A → A)
---------
    □A
```

**Proposed Diagonalization for I**:
```
I(IA → A)
---------
    IA
```

*Status*: Conjecture - requires proof or counterexample.

### Self-Reference Rules

**Self-Reference for I**:
```
IA
----
IIA
```

*Justification*: Direct application of axiom I2.

**Iteration Rule**:
```
   IA
-------
I^n A
```

where I^n A denotes n applications of I.

*Derivation*: Induction using axiom I2.

## Structural Rules

### Weakening and Strengthening

**Modal Weakening**: Not generally valid

**Structural Rules for Context**:
- **Exchange**: Order of premises doesn't matter
- **Contraction**: Duplicate premises can be merged  
- **Weakening**: Additional premises don't invalidate derivations

### Cut Rules

**Semantic Cut**:
```
Γ ⊢ A ∨ B, Γ, A ⊢ C, Γ, B ⊢ C
------------------------------
           Γ ⊢ C
```

**Modal Cut for □**:
```
Γ ⊢ □A ∨ ♢¬A, Γ, □A ⊢ C, Γ, ♢¬A ⊢ C
-----------------------------------
               Γ ⊢ C
```

**Modal Cut for I**:
```
Γ ⊢ IA ∨ ♦¬A, Γ, IA ⊢ C, Γ, ♦¬A ⊢ C
----------------------------------
              Γ ⊢ C
```

## Proof Strategies and Tactics

### Common Proof Patterns

**Pattern 1 - Inclusion Arguments**:
When proving IA from □A:
1. Apply axiom I3 directly
2. Use modus ponens

**Pattern 2 - Contrapositive Arguments**:
When proving ¬□A from ¬IA:
1. This is generally invalid
2. Requires careful semantic analysis

**Pattern 3 - Case Analysis**:
For formulas involving both □ and I:
1. Consider cases where □A holds vs. doesn't hold
2. Use inclusion properties to relate operators

### Proof Tactics

**Tactic 1 - Semantic Interpolation**:
When operators don't directly relate:
1. Construct intermediate formulas
2. Use frame properties
3. Apply semantic arguments

**Tactic 2 - Diagonalization**:
For fixed point constructions:
1. Apply standard diagonalization lemma
2. Extend to interface operator
3. Verify consistency

## Admissibility Results

### Admissible Rules

**Rule Schema**: A rule is admissible if adding it as a primitive rule doesn't increase the set of theorems.

**Theorem**: The following rules are admissible in GL+I:

1. **Substitution Rule**: If ⊢ A, then ⊢ A[B/p] for any formula B and variable p
2. **Replacement Rule**: If ⊢ A ↔ B, then ⊢ C ↔ C[B/A]  
3. **Modal Replacement**: If ⊢ A ↔ B, then ⊢ □A ↔ □B and ⊢ IA ↔ IB

### Non-Admissible Rules

**Counterexamples**:

1. **Löb Rule for I**: I(IA → A) ⊢ IA
   - Status: Unknown (requires investigation)

2. **Conversion Rule**: IA ⊢ □A  
   - Status: Not admissible (violates frame properties)

3. **Uniform Substitution for Modalities**: □A ⊢ IA[□/I]
   - Status: Not admissible (changes operator meaning)

## Complexity and Decidability

### Rule Application Complexity

**Decidability of Rule Application**:
- Checking if MP applies: O(1)
- Checking if Nec□ applies: O(n) where n is derivation length
- Checking if NecI applies: O(n)

**Search Space**:
- Modal rules increase search space exponentially
- Dual operators double the modal search space
- Heuristics needed for practical proof search

### Automated Proof Procedures

**Tableau Method Extensions**:
1. Extend GL tableau with I-rules
2. Handle inclusion condition R□ ⊆ RI
3. Maintain termination properties

**Resolution-Based Methods**:
1. Modal resolution for both operators
2. Inclusion resolution rules
3. Completeness preservation

This completes the comprehensive analysis of inference rules for GL+I, providing the foundation for proof construction and automated reasoning in the extended system.