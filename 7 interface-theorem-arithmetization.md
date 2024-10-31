# VI. Arithmetization

## A. Gödel Numbering

### Definition 12 (Basic Encoding)
We assign unique natural numbers to:

1. Basic Symbols:
```
Symbol | Gödel Number
---------------------
0      | 1
S      | 3
+      | 5
×      | 7
=      | 9
¬      | 11
∧      | 13
∨      | 15
→      | 17
↔      | 19
∀      | 21
∃      | 23
□      | 25
I      | 27
(      | 29
)      | 31
```

2. Variables:
   - For variable xₙ, assign number 2n+1
   - Ensures unique encoding for each variable

### Definition 13 (Compound Expressions)
For expressions e₁,...,eₙ with Gödel numbers g₁,...,gₙ:
```
⌜e₁e₂...eₙ⌝ = 2^g₁ × 3^g₂ × ... × p_n^gₙ
where p_n is the nth prime number
```

## B. Representability

### Definition 14 (Representability)
A relation R(x₁,...,xₙ) is representable in S if there exists a formula φ(x₁,...,xₙ) such that:

1. For any n-tuple (a₁,...,aₙ):
   If R(a₁,...,aₙ) is true:
   - S ⊢ φ(ā₁,...,āₙ)
   
2. For any n-tuple (a₁,...,aₙ):
   If R(a₁,...,aₙ) is false:
   - S ⊢ ¬φ(ā₁,...,āₙ)

Where āᵢ denotes the numeral for aᵢ

## C. Expressibility Results

### Lemma 4 (Basic Functions)
The following are representable in S:

1. Basic Arithmetic Functions:
   - Addition: x + y = z
   - Multiplication: x × y = z
   - Successor: S(x) = y

2. Syntactic Functions:
   - len(x): length of sequence with Gödel number x
   - concat(x,y): concatenation of sequences
   - sub(x,y,z): substitution function

### Lemma 5 (Key Predicates)
The following are representable in S:

1. Proof Predicates:
```
Prf(x,y): "x is the Gödel number of a proof of formula with Gödel number y"
Specifications:
a) S ⊢ Prf(⌜π⌝,⌜A⌝) if π is a proof of A
b) S ⊢ ¬Prf(n,⌜A⌝) if n is not a proof of A
```

2. Provability Predicate:
```
Prv(y): ∃xPrf(x,y)
Properties:
a) If S ⊢ A then S ⊢ Prv(⌜A⌝)
b) S ⊢ Prv(⌜A⌝) → □A
```

3. Interface Predicate:
```
Int(y): "Formula with Gödel number y is interface-accessible"
Properties:
a) S ⊢ Int(⌜A⌝) ↔ I(A)
b) Satisfies interface axioms
```

## D. Fixed Point Theorem

### Theorem 5 (Diagonal Lemma)
For any formula φ(x) with one free variable, there exists a sentence G such that:
```
S ⊢ G ↔ φ(⌜G⌝)
```

Proof:
```
1. Define diagonal function d(x):
   - Takes Gödel number of formula with one free variable
   - Returns Gödel number of formula with its own Gödel number substituted

2. Let ψ(x) be formula φ(d(x))

3. Let g = ⌜ψ(x)⌝

4. Let G be ψ(g)

5. Then:
   ⌜G⌝ = d(g)
   Therefore S ⊢ G ↔ φ(⌜G⌝)
```

### Corollary 1 (Interface Fixed Point)
There exists a formula G such that:
```
S ⊢ G ↔ ¬I(G)
```

This is the crucial sentence needed for our main theorem.

### Important Notes:
1. Arithmetization provides bridge between syntax and arithmetic
2. Representability ensures formal system can reason about its own syntax
3. Fixed point construction is essential for self-reference
4. Interface predicate connects syntactic and semantic aspects

