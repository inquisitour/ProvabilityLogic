# V. Key Properties and Fundamental Lemmas

## A. Fundamental Properties (Lemma 1)

### Lemma 1 (Basic Properties)
For any formulas A, B in system S:

1. Closure Properties:
   - If S ⊢ A and S ⊢ A → B, then S ⊢ B
   - If S ⊢ A, then S ⊢ □A
   - If S ⊢ A, then S ⊢ I(A)

2. Modal Properties:
   - S ⊢ □(A → B) → □A → □B
   - S ⊢ I(A → B) → I(A) → I(B)

Proof:
```
1. Closure Properties:
   a) First property by Modus Ponens
   b) Second property by Necessitation rule
   c) Third property:
      - From S ⊢ A, get S ⊢ □A by (b)
      - Use axiom I4: □A → I(A)
      - Apply Modus Ponens

2. Modal Properties:
   a) First property is axiom P1
   b) Second property is axiom I1
```

## B. Interface Structure (Lemma 2)

### Lemma 2 (Interface Properties)
For any Kripke model M = (W, R□, RI, V):

1. Structural Properties:
   - R□ ⊆ RI
   - RI is transitive
   - R□ is transitive

2. Semantic Consequences:
   - If M,w ⊨ □A then M,w ⊨ I(A)
   - If M,w ⊨ I(A) then M,w ⊨ A

Proof:
```
1. R□ ⊆ RI:
   - Take any w,v ∈ W where wR□v
   - By axiom I4: □A → I(A)
   - For any A, if M,w ⊨ □A then M,w ⊨ I(A)
   - This is only possible if wRIv
   - Therefore R□ ⊆ RI

2. RI is transitive:
   - Take any w,v,u ∈ W where wRIv and vRIu
   - Let M,w ⊨ I(A)
   - By axiom I3: I(A) → I(I(A))
   - Therefore M,w ⊨ I(I(A))
   - This implies M,v ⊨ I(A)
   - Which implies M,u ⊨ A
   - Therefore wRIu

3. R□ is transitive:
   - Similar proof using axiom P2: □A → □□A
```

## C. Derived Properties (Lemma 3)

### Lemma 3 (Interface-Provability Interaction)
The following properties hold in S:

1. S ⊢ I(A) → II(A)
2. S ⊢ □A → □I(A)
3. S ⊢ I□A → □A

Proof:
```
1. First property:
   - Use axiom I3: I(A) → I(I(A))

2. Second property:
   - From □A → I(A) (axiom I4)
   - Apply □ to both sides
   - Use P1 and P2

3. Third property:
   - From I(A) → A (axiom I2)
   - Substitute □A for A
   - Use properties of □
```

## D. Relationships Between Properties

### Theorem 4 (Completeness Properties)
The following relationships hold:

1. For any formula A:
   - If ⊨ A then S ⊢ A
   - If S ⊢ A then ⊨ A

2. For modal formulas:
   - S ⊢ □A → A implies S ⊢ A
   - S ⊢ I(A) → A is consistent

Proof:
```
1. First pair:
   - Soundness: standard induction on proofs
   - Completeness: canonical model construction

2. Second pair:
   - First implication by Löb's theorem
   - Second by semantic construction
```

### Important Notes
1. These lemmas form the technical foundation for our main theorem
2. The interaction between □ and I is crucial
3. These properties show the interface structure is well-behaved
4. The completeness properties ensure our system captures intended semantics

