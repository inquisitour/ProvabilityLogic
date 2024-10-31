# III. Semantic Framework

## A. Kripke Models

### Definition 6 (Kripke Model)
A Kripke model M for language L is a tuple (W, R□, RI, V) where:

1. Structure Components
   - W is a non-empty set (possible worlds)
   - R□ ⊆ W × W (provability accessibility relation)
   - RI ⊆ W × W (interface accessibility relation)
   - V is a valuation function

2. Valuation Function Properties
   V assigns to each world w ∈ W:
   - For each n-ary relation symbol R, an n-ary relation V(R,w) on the domain
   - For each n-ary function symbol f, an n-ary function V(f,w) on the domain
   - For each constant c, an element V(c,w) of the domain

3. Structural Requirements
   - R□ is transitive
   - RI is transitive
   - R□ ⊆ RI (reflecting axiom I4: □A → I(A))

## B. Satisfaction Relations

### Definition 7 (Satisfaction)
For any world w ∈ W and formula A, we define M,w ⊨ A inductively:

1. Atomic Formulas
   - M,w ⊨ t₁ = t₂ iff V(t₁,w) = V(t₂,w)
   - For n-ary relation R: M,w ⊨ R(t₁,...,tₙ) iff (V(t₁,w),...,V(tₙ,w)) ∈ V(R,w)

2. Modal Operators
   - M,w ⊨ □A iff ∀v(wR□v → M,v ⊨ A)
   - M,w ⊨ I(A) iff ∀v(wRIv → M,v ⊨ A)

3. Logical Connectives
   - M,w ⊨ ¬A iff not M,w ⊨ A
   - M,w ⊨ A ∧ B iff M,w ⊨ A and M,w ⊨ B
   - M,w ⊨ A ∨ B iff M,w ⊨ A or M,w ⊨ B
   - M,w ⊨ A → B iff M,w ⊨ A implies M,w ⊨ B
   - M,w ⊨ A ↔ B iff M,w ⊨ A if and only if M,w ⊨ B

4. Quantifiers
   - M,w ⊨ ∀xA iff for all d in the domain, M,w ⊨ A[d/x]
   - M,w ⊨ ∃xA iff there exists d in the domain such that M,w ⊨ A[d/x]

### Definition 8 (Truth and Validity)

1. Truth in a Model
   - A formula A is true in a model M (written M ⊨ A) iff M,w ⊨ A for all w ∈ W

2. Validity
   - A formula A is valid (written ⊨ A) iff A is true in all models
   - A formula A is valid in a frame F iff A is true in all models based on F

3. Semantic Consequence
   - B is a semantic consequence of A (written A ⊨ B) iff 
     for all models M and worlds w, if M,w ⊨ A then M,w ⊨ B

### Definition 9 (Special Properties)

1. Interface Properties
   - Truth Reflection: ⊨ I(A) → A
   - Interface Distribution: ⊨ I(A → B) → (I(A) → I(B))
   - Self-Reflection: ⊨ I(A) → I(I(A))
   - Provability Inclusion: ⊨ □A → I(A)

2. Frame Properties
   - R□ transitivity corresponds to axiom P2
   - RI transitivity corresponds to axiom I3
   - R□ ⊆ RI corresponds to axiom I4

### Notes
1. The relationship between R□ and RI captures the essential interface structure
2. The semantic conditions ensure soundness for our axiom system
3. These definitions provide foundation for both semantic and syntactic results
