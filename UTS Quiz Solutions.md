# Soal Latihan UTS Mat Dis (2026-09-25): Solutions

Worked solutions for `Soal latihan UTS Mat Dis 20260925.docx`, with the slide or page each method comes from.

> **Known errors in the quiz.** Question 2 (set sizes) and Question 3 (membership grades of 1.5) contain impossible data. Both are solved exactly as written using the method from the slides, and each problem is flagged where it occurs. Check the intended values with the lecturer.

---

## Question 1: Boolean Expression, Karnaugh Map, and Logic Circuit

**References:** *The Logic of Compound Statements.pptx*
- Slides 57–58: designing a circuit from an input/output table (sum-of-products / DNF)
- Slide 60: full DNF
- Slides 64–65: K-map basics, minterms, adjacent cells
- Slides 67–70: 3-variable K-map and blocks
- Slides 50, 56: NOT/AND/OR gates, building circuits from expressions

Truth table rows where S = 1:

| P | Q | R | S |
|---|---|---|---|
| 0 | 0 | 0 | **1** |
| 0 | 0 | 1 | 0 |
| 0 | 1 | 0 | **1** |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |
| 1 | 0 | 1 | **1** |
| 1 | 1 | 0 | 0 |
| 1 | 1 | 1 | **1** |

### a. Canonical SOP

For each row with S = 1, write a product of all three variables. Use the variable when its input is 1 and its complement (') when its input is 0 (slide 57 method).

| Row (PQR) | Product |
|---|---|
| 000 | P'Q'R' |
| 010 | P'QR' |
| 101 | PQ'R |
| 111 | PQR |

**S = P'Q'R' + P'QR' + PQ'R + PQR**

### b. Minterm notation

Each row's index is the binary value of PQR: 000 = 0, 010 = 2, 101 = 5, 111 = 7.

**S(P,Q,R) = Σm(0, 2, 5, 7)**

The slides define minterms (slide 65) but don't show the Σm shorthand. The shorthand is standard notation from Rosen, which the slides list as a reference.

### c. Karnaugh map

Columns are QR in Gray-code order (00, 01, 11, 10), so neighbouring cells differ by one variable. The left and right edges are adjacent.

| P \ QR | 00 | 01 | 11 | 10 |
|---|---|---|---|---|
| **0** | 1 (m0) | 0 (m1) | 0 (m3) | 1 (m2) |
| **1** | 0 (m4) | 1 (m5) | 1 (m7) | 0 (m6) |

Slide 67 may place the variables on different axes. The groups found below are the same in any layout.

### d. Simplest expression

- **Group 1:** m0 + m2 (row P = 0, wrapping around the edges). P = 0 and R = 0 stay fixed while Q changes, so the group gives **P'R'**.
- **Group 2:** m5 + m7 (row P = 1, middle columns). P = 1 and R = 1 stay fixed while Q changes, so the group gives **PR**.

**S = P'R' + PR**

Check by algebra: P'Q'R' + P'QR' = P'R'(Q' + Q) = P'R', and PQ'R + PQR = PR(Q' + Q) = PR.

Q has no effect on the output. The result is P XNOR R, the negation of the exclusive-or expression (P ∨ R) ∧ ∼(P ∧ R) from slide 54.

### e. Logic circuit

Gates needed: 2 NOT, 2 AND (2-input), 1 OR (2-input). Q is not connected.

```
P ──●─────────────────────┐
    │                    [AND]── PR ────┐
R ──┼──●──────────────────┘             │
    │  │                               [OR]── S
    └[NOT]── P' ──────────┐             │
       │                 [AND]── P'R' ──┘
       └[NOT]── R' ───────┘
```

---

## Question 2: Set Theory

**References:** *Set Theory.pptx*
- Slide 20: Inclusion/Exclusion Rule for 3 sets
- Slide 22: worked survey example with the same four sub-questions (none, all three, "X and Y but not Z", "only X")

Rule:

N(M∪S∪L) = N(M) + N(S) + N(L) − N(M∩S) − N(M∩L) − N(S∩L) + N(M∩S∩L)

### a. All three subjects

50 = 50 + 15 + 32 − 30 − 20 − 25 + x
50 = 22 + x
**x = |M∩S∩L| = 28**

### b. None of the three

100 − |M∪S∪L| = 100 − 50 = **50**

### c. Math and Science but not Literature

|M∩S| − |M∩S∩L| = 30 − 28 = **2**

### d. Only Science

Fill the Venn diagram from the centre outward:

| Region | Calculation | Value |
|---|---|---|
| M∩S∩L | (a) | 28 |
| M∩S only | 30 − 28 | 2 |
| M∩L only | 20 − 28 | −8 |
| S∩L only | 25 − 28 | −3 |
| M only | 50 − 2 − (−8) − 28 | 28 |
| **S only** | 15 − 2 − (−3) − 28 | **−12** |
| L only | 32 − (−8) − (−3) − 28 | 15 |
| Total | | 50 ✔ |

**Only Science = −12**

> ⚠️ **The data is inconsistent.** An intersection can't be larger than either set in it, but |M∩S| = 30 and |S∩L| = 25 are both larger than |S| = 15. The three-subject count of 28 is also larger than |M∩L| = 20. That's why three Venn regions come out negative. The method is correct, but the numbers in the question are wrong.

---

## Question 3: Fuzzy Set

**References:**
- *Properties of Functions and Fuzzy Set.pptx*, slide 37: union = max, intersection = min, complement = 1 − μ
- Same deck, slide 39: support (μ > 0)
- Same deck, slide 40: α-cut (μ ≥ α)
- Same deck, slide 43: worked discrete example (support, α-cuts, union, intersection)
- *Fuzzy Set.pdf*, page 4: membership must satisfy μ : X → [0, 1]

Data as written:
A = {0.1/15, 1.5/25, 0.8/35, 1.5/45, 0.6/55}
B = {0.7/15, 0.4/25, 0.8/35, 1.5/45, 0.1/55}

| x | μA | μB | A∪B = max | A∩B = min | Aᶜ = 1 − μA |
|---|---|---|---|---|---|
| 15 | 0.1 | 0.7 | 0.7 | 0.1 | 0.9 |
| 25 | 1.5 | 0.4 | 1.5 | 0.4 | −0.5 |
| 35 | 0.8 | 0.8 | 0.8 | 0.8 | 0.2 |
| 45 | 1.5 | 1.5 | 1.5 | 1.5 | −0.5 |
| 55 | 0.6 | 0.1 | 0.6 | 0.1 | 0.4 |

### a. A ∪ B
**A∪B = 0.7/15 + 1.5/25 + 0.8/35 + 1.5/45 + 0.6/55**

### b. A ∩ B
**A∩B = 0.1/15 + 0.4/25 + 0.8/35 + 1.5/45 + 0.1/55**

### c. Complement Aᶜ
**Aᶜ = 0.9/15 + (−0.5)/25 + 0.2/35 + (−0.5)/45 + 0.4/55**

### d. Support of A
All five elements have μA > 0.
**supp(A) = {15, 25, 35, 45, 55}**

### e. 0.6-cut of A

The docx stops at "denoted" because the equation is missing. It is probably A₀.₆.

Keep the elements with μA ≥ 0.6. That gives 25 (1.5), 35 (0.8), 45 (1.5) and 55 (0.6, included because the test is ≥).
**A₀.₆ = {25, 35, 45, 55}**

> ⚠️ **1.5 is not a valid membership grade.** Grades must be between 0 and 1, which is why the complement comes out negative.
>
> If 1.5 was meant to be **0.5**, the answers become:
> - A∪B = 0.7/15 + 0.5/25 + 0.8/35 + 0.5/45 + 0.6/55
> - A∩B = 0.1/15 + 0.4/25 + 0.8/35 + 0.5/45 + 0.1/55
> - Aᶜ = 0.9/15 + 0.5/25 + 0.2/35 + 0.5/45 + 0.4/55
> - supp(A) = {15, 25, 35, 45, 55}
> - A₀.₆ = {35, 55}

---

## Question 4: Properties of Relations

**References:** *Properties of Relation.pptx*
- Slides 14–16: reflexive, symmetric, transitive (worked on finite sets)
- Slide 30: antisymmetry definition
- Slides 32–33: antisymmetry of the "divides" relation
- Slides 34–35: partial order definition, "divides" as a partial order
- Slides 36–38: building a Hasse diagram (divides example on {1, 2, 3, 9, 18})
- Slides 43–44: maximal, minimal, greatest, least elements

A = {5, 10, 13, 16, 22}, with aRb ⟺ a | b.

### a. R as ordered pairs

Check every pair (a, b):
- Every element divides itself.
- 5 | 10 (10 = 5·2).
- 5 doesn't divide 13, 16 or 22. 10 doesn't divide 13, 16 or 22. 13 doesn't divide 16 or 22. 16 doesn't divide 22.
- A larger number can't divide a smaller positive one.

**R = {(5,5), (10,10), (13,13), (16,16), (22,22), (5,10)}**

### b. Properties

| Property | Holds? | Justification |
|---|---|---|
| Reflexive | **Yes** | a \| a for every a ∈ A, so all five (a,a) pairs are in R. |
| Symmetric | **No** | (5,10) ∈ R but (10,5) ∉ R, because 10 doesn't divide 5. |
| Antisymmetric | **Yes** | The only pair with a ≠ b is (5,10), and its reverse isn't in R. For positive integers, a \| b and b \| a imply a = b (slide 32). |
| Transitive | **Yes** | The only chains aRb, bRc are 5→5→10 and 5→10→10. Both give (5,10) ∈ R. Chains through loops are trivial. |

### c. Partial order?

**Yes.** R is reflexive, antisymmetric and transitive, which is the definition of a partial order (slide 34).

### d. Hasse diagram

Steps from slide 36: draw the directed graph with arrows pointing upward, remove the loops, remove arrows implied by transitivity (there are none here), then remove the arrowheads.

```
   10
   |
   5        13        16        22
```

10 sits above 5. 13, 16 and 22 are isolated points because they aren't comparable to any other element.

### e. Special elements

| | Answer | Reason |
|---|---|---|
| Minimal | **5, 13, 16, 22** | Nothing lies below them. |
| Maximal | **10, 13, 16, 22** | Nothing lies above them. |
| Least | **None** | No single element divides every element of A. |
| Greatest | **None** | No single element is divisible by every element of A. |
