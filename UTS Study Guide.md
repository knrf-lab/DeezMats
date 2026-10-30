# Discrete Math Midterm (UTS) Study Guide

This guide covers the theory and formulas from the course materials in this repo, with the slide or page each item comes from. The midterm practice quiz covers K-maps, sets, fuzzy sets and relations, so those sections include step-by-step methods. Worked answers are in [`UTS Quiz Solutions.md`](UTS%20Quiz%20Solutions.md).

**File key**

| Short name | File |
|---|---|
| CS | `The Logic of Compound Statements.pptx` (Sessions 1–3) |
| QS | `The Logic of Quantified Statements.pptx` (Session 4) |
| MP | `Elementary Number Theory and Methods of Proof.pptx` (Sessions 5–6) |
| ST | `Set Theory.pptx` (Sessions 7–8) |
| FF | `Properties of Functions and Fuzzy Set.pptx` (Sessions 11–12) |
| PR | `Properties of Relation.pptx` (Sessions 13–14) |
| NT | `Introduction to Number Theory and its Applications.pdf` |
| FZ | `Fuzzy Set.pdf` |
| RP | `Relations and Partial Orders.pdf` |
| PL / PdL | `Propositional Logic.pdf` / `Predicate Logic.pdf` |

---

## 1. Logic of Compound Statements (CS)

### Connectives (CS slides 7–11, 19, 25)

| p | q | ∼p | p∧q | p∨q | p⊕q | p→q | p↔q |
|---|---|---|---|---|---|---|---|
| T | T | F | T | T | F | T | T |
| T | F | F | F | T | T | F | F |
| F | T | T | F | T | T | T | F |
| F | F | T | F | F | F | T | T |

- **Order of operations** (slide 26): ∼ first, then ∧ and ∨ (use parentheses between them), then → and ↔.
- **Vacuously true** (slide 20): p→q is true whenever p is false.

### Logical equivalences (slide 16, Epp Theorem 2.1.1)

| Law | Form |
|---|---|
| Commutative | p∧q ≡ q∧p; p∨q ≡ q∨p |
| Associative | (p∧q)∧r ≡ p∧(q∧r); same for ∨ |
| Distributive | p∧(q∨r) ≡ (p∧q)∨(p∧r); p∨(q∧r) ≡ (p∨q)∧(p∨r) |
| Identity | p∧t ≡ p; p∨c ≡ p |
| Negation | p∨∼p ≡ t; p∧∼p ≡ c |
| Double negation | ∼(∼p) ≡ p |
| Idempotent | p∧p ≡ p; p∨p ≡ p |
| Universal bound | p∨t ≡ t; p∧c ≡ c |
| De Morgan | ∼(p∧q) ≡ ∼p∨∼q; ∼(p∨q) ≡ ∼p∧∼q |
| Absorption | p∨(p∧q) ≡ p; p∧(p∨q) ≡ p |
| Negations of t, c | ∼t ≡ c; ∼c ≡ t |

- **Tautology:** always true. **Contradiction:** always false (slide 15).
- To show two forms are **not equivalent**, find one truth-table row where they differ (slide 14).

### Conditionals (slides 19–31)

- p→q ≡ ∼p∨q
- **Negation:** ∼(p→q) ≡ p∧∼q (slide 21)
- **Contrapositive** ∼q→∼p ≡ p→q
- **Converse** q→p and **inverse** ∼p→∼q are equivalent to each other but not to p→q (slides 22–24)
- p↔q ≡ (p→q)∧(q→p) (slide 27)
- "p only if q" means p→q
- "r is a **sufficient** condition for s" means r→s (slide 30)
- "r is a **necessary** condition for s" means ∼r→∼s, which is equivalent to s→r (slide 31)

### Valid arguments (slides 33–45)

Method (slide 34):
1. Build a truth table with all premises and the conclusion.
2. Mark the **critical rows**, where every premise is true.
3. If any critical row has a false conclusion, the argument is **invalid**. Otherwise it is **valid**.

**Rules of inference** (slide 37):

| Rule | Form |
|---|---|
| Modus ponens | p→q, p ∴ q |
| Modus tollens | p→q, ∼q ∴ ∼p |
| Generalization | p ∴ p∨q |
| Specialization | p∧q ∴ p |
| Elimination | p∨q, ∼q ∴ p |
| Transitivity | p→q, q→r ∴ p→r |
| Division into cases | p∨q, p→r, q→r ∴ r |
| Contradiction rule | ∼p→c ∴ p |

**Fallacies** (slides 41–43):
- **Converse error** (affirming the consequent): p→q, q ∴ p
- **Inverse error** (denying the antecedent): p→q, ∼p ∴ ∼q

Valid means the conclusion follows from the premises. It does not mean the premises or the conclusion are true (slides 44–45).

### Digital logic circuits (slides 46–58)

- Gates: NOT = ∼, AND = ∧, OR = ∨ (slide 50). NAND = ∼(P∧Q) and NOR = ∼(P∨Q) (slide 51).
- **Circuit → expression:** work from the inputs to the output, labelling each gate's output (slide 54).
- **Expression → circuit:** build innermost parentheses first (slide 56).
- **Table → circuit** (slides 57–58):
  1. Find the rows where the output is 1.
  2. Write one AND term per row (variable if 1, complement if 0).
  3. OR the terms together. The result is the **sum-of-products** form, also called **DNF**.

### Boolean simplification (slides 59–62)

- **DNF:** no product term contains another (slide 59).
- **Full DNF:** every product term contains every variable. To expand a term, multiply it by (Y + Y') (slide 60).
- **Consensus:** if two products differ in exactly one complemented variable, their consensus is the product of the remaining literals (slide 61).
- **Inclusion:** if P2 contains P1, then P1 + P2 = P1 (slide 62).

### Karnaugh maps (slides 63–74)

- **Minterm:** a product that contains every variable once. Minterm index = binary value of the inputs, e.g. PQ'R = 101 = m5. Notation: Σm(…).
- **Layout:** label columns in Gray-code order (00, 01, 11, 10) so adjacent cells differ by one literal. The edges wrap around (slide 65).
- **Procedure:**
  1. Put a 1 in the cell for each minterm.
  2. Cover every 1 using the **largest** possible rectangular blocks of size 1, 2, 4 or 8 (slides 68, 72). Blocks may overlap.
  3. Use as **few** blocks as possible.
  4. In each block, drop any variable that changes value. Keep the variables that stay fixed.
  5. OR the block terms together.
- **Block sizes:**

| Variables | Block of 2 removes | Block of 4 removes | Block of 8 removes |
|---|---|---|---|
| 3 variables | 1 variable | 2 variables | (whole map = 1) |
| 4 variables | 1 variable | 2 variables | 3 variables |

- **Common patterns:**
  - x'z' + xz is XNOR (equal inputs).
  - x'z + xz' is XOR.
  - XOR expanded: (P∨Q)∧∼(P∧Q) (slide 54).

---

## 2. Quantified Statements (QS)

- **Predicate:** a sentence with variables that becomes a statement once values are substituted. **Truth set:** the values that make it true (slides 6–8).
- **∀x∈D, Q(x)** is true iff Q(x) holds for every x. One counterexample makes it false (slides 10–12).
- **∃x∈D, Q(x)** is true iff Q(x) holds for at least one x (slides 13–15).
- **Universal conditional:** ∀x, P(x)→Q(x) (slide 19).

### Negations (slides 21–24, 33)

| Statement | Negation |
|---|---|
| ∀x, Q(x) | ∃x such that ∼Q(x) |
| ∃x, Q(x) | ∀x, ∼Q(x) |
| ∀x, P(x)→Q(x) | ∃x such that P(x) ∧ ∼Q(x) |
| ∀x ∃y, P(x,y) | ∃x ∀y, ∼P(x,y) |
| ∃x ∀y, P(x,y) | ∀x ∃y, ∼P(x,y) |

- "No A are B" means ∀x∈A, x is not B. Its negation is "Some A are B" (slide 23).
- **Quantifier order matters** (slide 28):
  - ∀x∃y: for each x, y may be different.
  - ∃x∀y: one fixed x works for every y.
- See also PdL pages 6 and 9.

---

## 3. Methods of Proof and Induction (MP)

**Useful definitions:**
- Even: n = 2k. Odd: n = 2k + 1.
- Rational: r = p/q with p, q integers and q ≠ 0 (slide 9).

**Proof methods:**

| Method | How it works | Slides |
|---|---|---|
| Direct | Assume p, derive q. | 6–10 |
| Contraposition | Prove ∼q→∼p instead. Example: "3n+2 odd ⇒ n odd" by assuming n = 2k. | 12–15 |
| Contradiction | Assume the statement is false and derive something impossible. Example: rational + irrational = irrational. | 16–18 |
| Counterexample | To disprove ∀x, P(x)→Q(x), find one x where P(x) is true and Q(x) is false. | 19–21 |

**Mathematical induction** (slides 22–29):
1. **Basis step:** prove P(1).
2. **Inductive step:** assume P(k) (the inductive hypothesis) and prove P(k+1).
3. Standard example: 1 + 2 + … + n = n(n+1)/2. Add (k+1) to both sides of P(k), then simplify to (k+1)(k+2)/2.

---

## 4. Number Theory (NT)

No slide deck covers this topic (see the repo notes at the end), so this section uses the PDF.

| Topic | Key facts | NT page |
|---|---|---|
| Divisibility | a \| b ⟺ b = ak. If a \| b and a \| c, then a \| (b + c) and a \| bc. | 3–4 |
| Division algorithm | a = dq + r, 0 ≤ r < d. q = a div d, r = a mod d. | 5 |
| Congruence | a ≡ b (mod m) ⟺ m \| (a − b) ⟺ a mod m = b mod m. | 9–10 |
| Congruence arithmetic | If a ≡ b and c ≡ d (mod m), then a + c ≡ b + d and ac ≡ bd (mod m). | 10–11 |
| Hashing | h(k) = k mod m | 13 |
| Caesar cipher | f(p) = (p + 3) mod 26; decrypt with (p − 3) mod 26. | 15 |
| Fundamental Theorem of Arithmetic | Every integer > 1 is a unique product of primes. | 17 |
| Primality test | If n is composite, it has a prime divisor ≤ √n. | 18 |
| gcd / lcm | From prime factorisations, gcd uses min exponents and lcm uses max exponents. ab = gcd(a,b)·lcm(a,b). | 20–24 |
| Euclidean algorithm | gcd(a, b) = gcd(b, a mod b). Repeat until the remainder is 0. | 26–29 |
| Bézout / Extended Euclid | gcd(a,b) = sa + tb for some integers s, t. | 30–31 |
| Modular inverse | ā exists iff gcd(a, m) = 1, and aā ≡ 1 (mod m). | 34–36 |
| Linear congruence | Solve ax ≡ b (mod m) by multiplying both sides by ā. | 34 |

---

## 5. Set Theory (ST)

### Basic definitions (slides 7–12)

- **Sets are unordered** and repetition doesn't count: {1,1,2} = {1,2}.
- **Subset:** A ⊆ B. The empty set ∅ is a subset of every set.
- **Cardinality:** |S| = number of distinct elements.
- **Power set:** P(S) is the set of all subsets, and |P(S)| = 2^|S|.
- **Cartesian product:** A × B = {(a,b) | a∈A, b∈B}, and |A×B| = |A|·|B|.

### Operations (slides 14–18)

| Operation | Definition |
|---|---|
| A ∪ B | x∈A ∨ x∈B |
| A ∩ B | x∈A ∧ x∈B |
| Aᶜ | x∉A |
| A − B | A ∩ Bᶜ |
| Disjoint | A ∩ B = ∅ |

### Identities (slides 23–24)

- Identity: A∪∅ = A, A∩U = A
- Domination: A∪U = U, A∩∅ = ∅
- Idempotent: A∪A = A, A∩A = A
- Commutative and associative laws for ∪ and ∩
- Distributive: A∪(B∩C) = (A∪B)∩(A∪C), A∩(B∪C) = (A∩B)∪(A∩C)
- Complement: A∪Aᶜ = U, A∩Aᶜ = ∅, (Aᶜ)ᶜ = A
- De Morgan: (A∪B)ᶜ = Aᶜ∩Bᶜ, (A∩B)ᶜ = Aᶜ∪Bᶜ

### Inclusion / Exclusion (slides 20–22)

- N(A∪B) = N(A) + N(B) − N(A∩B)
- N(A∪B∪C) = N(A) + N(B) + N(C) − N(A∩B) − N(A∩C) − N(B∩C) + N(A∩B∩C)

**Survey-problem method** (slide 22):
1. **All three:** solve the 3-set formula for N(A∩B∩C).
2. **None:** total − N(A∪B∪C).
3. **A and B but not C:** N(A∩B) − N(A∩B∩C).
4. **Only A:** N(A) − N(A∩B) − N(A∩C) + N(A∩B∩C).
5. **Sanity check:** every Venn region must be ≥ 0. Every pairwise intersection must be ≤ both sets in it, and the triple intersection must be ≤ every pairwise intersection.

---

## 6. Functions (FF slides 5–31)

- **Function f: X → Y:** every x maps to exactly one y. Know domain, co-domain, range and inverse image (slides 6–9).
- **One-to-one (injective):** f(x₁) = f(x₂) ⇒ x₁ = x₂. To prove it, assume f(x₁) = f(x₂) and solve. To disprove it, find two different inputs with the same output (slides 11–14).
- **Onto (surjective):** for every y ∈ Y there is an x with f(x) = y. To prove it, solve y = f(x) for x and check that x is in the domain. Example: f(x) = 4x − 1 is onto over ℝ but not over ℤ, because 1/4 ∉ ℤ (slides 15–19).
- **Bijection:** a function that is both one-to-one and onto (slides 20–23).
- **Inverse:** f⁻¹(y) = x ⟺ f(x) = y. It exists only for bijections. Example: f(x) = 4x − 1 gives f⁻¹(y) = (y + 1)/4 (slides 24–26).
- **Composition:** (g∘f)(x) = g(f(x)). It requires range(f) ⊆ domain(g) (slides 28–31).

---

## 7. Fuzzy Sets (FF slides 32–47; FZ)

- **Membership grade:** μA(x) ∈ **[0, 1]** (FZ page 4). Any value outside this range is invalid.
- **Discrete notation:** A = μ₁/x₁ + μ₂/x₂ + … . The "/" is a separator, not division (FF slide 35).

| Concept | Formula | Source |
|---|---|---|
| Union | μA∪B(x) = max(μA(x), μB(x)) | FF 37 |
| Intersection | μA∩B(x) = min(μA(x), μB(x)) | FF 37 |
| Complement | μAᶜ(x) = 1 − μA(x) | FF 37 |
| Equality | A = B ⟺ μA(x) = μB(x) for all x | FF 38 |
| Subset | A ⊆ B ⟺ μA(x) ≤ μB(x) for all x | FF 38 |
| Support | supp(A) = {x \| μA(x) > 0}. An empty support means an empty fuzzy set. | FF 39 |
| α-cut | Aα = {x \| μA(x) ≥ α} | FF 40 |
| Strict α-cut | {x \| μA(x) > α} | FZ 6 |
| Cardinality | \|A\| = Σ μA(x) | FF 41 |
| Core | {x \| μA(x) = 1} | FZ 16 |
| Height | h(A) = max μA(x). A is normal if h = 1. | FZ 17 |

- Worked discrete example (support, α-cuts, ∪, ∩): FF slides 42–43.
- Continuous example: FF slides 44–47.
- **Tip** (general fuzzy-set fact, not on the slides): De Morgan works for fuzzy sets with max/min, e.g. (A∪B)ᶜ = Aᶜ∩Bᶜ. The law of excluded middle doesn't: A∪Aᶜ is not always all 1s.

---

## 8. Relations (PR; RP)

### Basics (PR slides 6–12)

- **Binary relation:** a subset of A × B. A relation on A is a subset of A × A.
- **Inverse:** R⁻¹ = {(b,a) | (a,b) ∈ R}.
- **Directed graph:** draw an arrow from a to b for each pair, and a loop for each (a,a).

### Properties (slides 14–21, 30–33)

| Property | Definition | Check on a digraph |
|---|---|---|
| Reflexive | (a,a) ∈ R for all a | Every vertex has a loop. |
| Symmetric | aRb ⇒ bRa | Every arrow has a reverse arrow. |
| Antisymmetric | aRb ∧ bRa ⇒ a = b | No pair of distinct vertices has arrows both ways. |
| Transitive | aRb ∧ bRc ⇒ aRc | Every two-step path has a shortcut arrow. |

- One counterexample is enough to disprove a property.
- A relation can be neither symmetric nor antisymmetric, or both at once (for example, only loops).
- On positive integers, "divides" is antisymmetric. On all integers it is not, because 2 | −2 and −2 | 2 (slides 32–33).

### Equivalence relations (slides 22–28)

- **Definition:** reflexive + symmetric + transitive.
- **Equivalence class:** [a] = {x ∈ A | x R a}.
- The distinct classes partition A (worked example: slide 28).

### Partial orders (slides 29–47; RP pages 10–16)

- **Partial order:** reflexive + **antisymmetric** + transitive (slide 34). Standard examples: ≤ on ℝ, | on ℤ⁺, ⊆ on sets.
- **Comparable:** a ≼ b or b ≼ a. **Total order:** every pair is comparable, e.g. ≤ on ℤ (slides 40–41).
- **Hasse diagram** (slide 36):
  1. Draw the digraph with all arrows pointing up.
  2. Remove the loops.
  3. Remove arrows implied by transitivity.
  4. Remove the arrowheads.
  5. Elements unrelated to anything are isolated points.

**Special elements** (slides 43–47):

| Term | Meaning |
|---|---|
| Maximal | Nothing is above it (there can be several). |
| Minimal | Nothing is below it (there can be several). |
| Greatest | Above **every** element. It is unique if it exists. |
| Least | Below **every** element. It is unique if it exists. |
| Upper bound of S | An element ≥ every element of S. |
| Lower bound of S | An element ≤ every element of S. |
| LUB | The smallest upper bound. |
| GLB | The largest lower bound. |

- If there are two or more maximal elements, there is no greatest element. The same goes for minimal and least.
- If two upper bounds are incomparable, there is no LUB (slide 47).

---

## 9. Exam checklist by question type

| Question type | Steps | Main source |
|---|---|---|
| Truth table → SOP → minterms → K-map → simplify → circuit | List rows with output 1 → write the products → Σm → Gray-code K-map → largest blocks → draw NOT/AND/OR | CS 57–58, 64–70, 50 |
| 3-set survey | Inclusion/exclusion → fill the Venn diagram centre-out → read off the regions | ST 20–22 |
| Fuzzy operations | max / min / 1 − μ per element → support (> 0) → α-cut (≥ α) | FF 37–43 |
| Relation properties → partial order → Hasse | List pairs → check R/S/A/T with counterexamples → draw Hasse → maximal/minimal/greatest/least | PR 14–44 |
| Negate a quantified statement | Flip ∀ and ∃, negate the predicate. ∼(P→Q) becomes P∧∼Q. | QS 21–24, 33 |
| Prove or disprove | Direct, contraposition, contradiction, counterexample, or induction | MP 6–29 |
| Argument validity | Truth table with critical rows, or a chain of inference rules | CS 33–40 |

---

## Repo notes

- `Mathematical Induction and Recursion.pptx` is a byte-for-byte copy of `Elementary Number Theory and Methods of Proof.pptx`. The actual recursion slides are missing, and that deck has no number theory slides, so section 4 uses the NT PDF.
- `Set Theory.pptx` is an older deck (2015, Epp 4th edition). The other decks are from 2021 (Epp 5th edition).
- No deck is labelled Sessions 9–10, so the midterm scope for those sessions is unclear.
- Many slides are images. Some citations in this guide point to a slide's title or topic rather than an exact formula.
