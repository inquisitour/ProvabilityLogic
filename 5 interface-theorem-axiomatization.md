# IV. Formal System and Axiomatization

## A. Basic Axioms

### 1. First-Order Logic Axioms
All instances of:

a) Propositional Axioms
   - A → (B → A)
   - (A → (B → C)) → ((A → B) → (A → C))
   - (¬B → ¬A) → ((¬B → A) → B)

b) Quantifier Axioms
   - ∀x(A → B) → (∀xA → ∀xB)
   - A → ∀xA (if x is not free in A)
   - ∀xA → A[t/x] (if t is free for x in A)
   - ∀x(x = x)
   - x = y → (A[x/z] → A[y/z]) (where A[x/z] results from replacing some occurrences of z by x)

### 2. Robinson Arithmetic (Q) Axioms

Q1. ∀x¬(0 = S(x))
   - Zero is not the successor of any number

Q2. ∀x∀y(S(x) = S(y) → x = y)
   - Successor function is injective

Q3. ∀x(x ≠ 0 → ∃y(x = S(y)))
   - Every non-zero number is a successor

Q4. ∀x∀y(x + 0 = x)
   - Addition with zero

Q5. ∀x∀y(x + S(y) = S(x + y))
   - Addition with successor

Q6. ∀x(x × 0 = 0)
   - Multiplication by zero

Q7. ∀x∀y(x × S(y) = (x × y) + x)
   - Multiplication by successor

## B. Modal Axioms

### 1. Provability Axioms (GL)

P1. □(A → B) → (□A → □B)
   - Distribution of provability over implication
   - Reflects closure under modus ponens

P2. □A → □□A
   - Provable provability is provable
   - Reflects proof checking

P3. □(□A → A) → □A
   - Löb's theorem
   - Reflects proof by contradiction with provability

### 2. Interface Axioms

I1. I(A → B) → (I(A) → I(B))
   - Distribution of interface over implication
   - Preserves logical structure through interface

I2. I(A) → A
   - Truth reflection
   - Interface-accessible statements are true

I3. I(A) → I(I(A))
   - Self-reflection
   - Interface awareness is interface-accessible

I4. □A → I(A)
   - Provability inclusion
   - Provable statements are interface-accessible

## C. Rules of Inference

### 1. Modus Ponens (MP)
From A and A → B, infer B
```
A    A → B
-----------
     B
```

### 2. Universal Generalization (UG)
From A, infer ∀xA (if x is not free in any assumption)
```
    A
---------
   ∀xA
```

### 3. Necessitation (Nec)
From ⊢ A, infer ⊢ □A (if A is provable without assumptions)
```
⊢ A
-------
⊢ □A
```

## D. Proof Definition

### Definition 10 (Formal Proof)
A proof in S is a finite sequence of formulas A₁,...,Aₙ where each Aᵢ is either:
1. An axiom of S
2. Follows from previous formulas by a rule of inference

### Definition 11 (Provability)
- We write S ⊢ A if there exists a proof of A in S
- A formula A is provable in S if S ⊢ A
- A formula A is refutable in S if S ⊢ ¬A
- A formula A is undecidable in S if neither A nor ¬A is provable in S

### Important Notes
1. The system is properly formalized with explicit syntax
2. All rules preserve validity
3. The system is sound with respect to our semantics
4. The interaction between □ and I is crucial for our main results
