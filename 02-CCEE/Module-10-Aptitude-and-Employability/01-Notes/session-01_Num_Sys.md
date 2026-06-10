# Session 01 — Number System 🔢

> **Module:** Aptitude & Effective Communication
> **Part:** I — Aptitude
> **File:** `session-01_Num_Sys.md`
> **Exam:** CCEE | 15–17 July 2026

---

## 📑 Table of Contents

- [1. Number System — Classification](#1-number-system--classification)
- [2. Unit Digit](#2-unit-digit)
- [3. Last 2 Digits](#3-last-2-digits)
- [4. Remainder](#4-remainder)
- [5. Divisibility Rules](#5-divisibility-rules)
- [6. Cyclicity](#6-cyclicity)
- [7. Fast Maths](#7-fast-maths)
- [8. Simplification (BODMAS)](#8-simplification-bodmas)
- [9. LCM & HCF](#9-lcm--hcf)
- [📌 Extra Notes](#-extra-notes)
- [🔤 Abbreviations Table](#-abbreviations-table)
- [🧠 Keywords + Concept Map](#-keywords--concept-map)
- [⚡ Quick Reference Cheatsheet](#-quick-reference-cheatsheet)
- [🔁 Session Revision Snapshot](#-session-revision-snapshot)

---

## 1. Number System — Classification

```
Numbers
├── Real Numbers
│   ├── Rational Numbers (p/q form, q≠0)
│   │   ├── Integers
│   │   │   ├── Negative Integers  → ..., -3, -2, -1
│   │   │   ├── Zero               → 0
│   │   │   └── Positive Integers (Natural Numbers) → 1, 2, 3, ...
│   │   │       └── Whole Numbers  → 0, 1, 2, 3, ...
│   │   └── Fractions              → 1/2, 3/4, ...
│   └── Irrational Numbers         → √2, √3, π, e
└── Imaginary Numbers              → √(-1) = i
```

### Key Definitions

| Term | Definition |
|---|---|
| Natural Numbers | Counting numbers starting from 1 → {1, 2, 3, ...} |
| Whole Numbers | Natural numbers including 0 → {0, 1, 2, 3, ...} |
| Integers | All whole numbers + negative numbers → {..., -2, -1, 0, 1, 2, ...} |
| Rational Number | Any number expressible as p/q where p, q are integers and q ≠ 0 |
| Irrational Number | Cannot be expressed as p/q — non-terminating, non-repeating decimals |
| Prime Number | Divisible only by 1 and itself. Smallest prime = **2** (only even prime) |
| Composite Number | Has more than two factors. Smallest composite = **4** |
| Co-prime Numbers | Two numbers whose HCF = 1. Example: (8, 9) |
| Perfect Number | Sum of all its factors (excluding itself) = the number. Example: 6 (1+2+3=6) |
| Twin Primes | Pair of primes differing by 2. Example: (3,5), (11,13), (17,19) |

> [!NOTE]
> **1 is neither prime nor composite.**
> **2 is the only even prime number.**
> 0 is neither positive nor negative.

---

## 2. Unit Digit

The **unit digit** of a product or power depends only on the unit digits of the base numbers involved.

### Unit Digit of Powers — Patterns

| Base Unit Digit | Cyclicity | Pattern |
|---|---|---|
| 0 | 1 | Always **0** |
| 1 | 1 | Always **1** |
| 2 | 4 | 2, 4, 8, 6, 2, 4, 8, 6... |
| 3 | 4 | 3, 9, 7, 1, 3, 9, 7, 1... |
| 4 | 2 | 4, 6, 4, 6... |
| 5 | 1 | Always **5** |
| 6 | 1 | Always **6** |
| 7 | 4 | 7, 9, 3, 1, 7, 9, 3, 1... |
| 8 | 4 | 8, 4, 2, 6, 8, 4, 2, 6... |
| 9 | 2 | 9, 1, 9, 1... |

### How to Find Unit Digit of aⁿ

1. Take only the **unit digit** of the base `a`
2. Find the **cyclicity** of that digit
3. Divide the **power n** by the cyclicity
4. The **remainder** tells you the position in the pattern
5. If remainder = 0 → take the **last value** in the cycle

#### Example
> Find unit digit of **7⁹⁵**
> - Unit digit of base = 7
> - Cyclicity of 7 = 4 → pattern: 7, 9, 3, 1
> - 95 ÷ 4 = 23 remainder **3**
> - 3rd position in (7, 9, 3, 1) = **3**
> - Unit digit = **3** ✅

### Unit Digit of a Product

> Unit digit of (123 × 456 × 789)
> = Unit digit of (3 × 6 × 9)
> = Unit digit of (18 × 9)
> = Unit digit of (162)
> = **2** ✅

---

## 3. Last 2 Digits

Last 2 digits = the **tens digit + unit digit** = remainder when divided by **100**

### Rules for Last 2 Digits of Powers

#### Case 1 — Last digit is 1
> Any number ending in 1 raised to any power:
> - Unit digit = always **1**
> - Tens digit = (tens digit of base × unit digit of power) mod 10

**Example:** Last 2 digits of **31⁷⁸⁶**
- Unit digit = 1
- Tens digit = (3 × 6) mod 10 = 18 mod 10 = **8**
- Last 2 digits = **81** ✅

#### Case 2 — Last digit is 3, 7, or 9
- Convert to a number ending in 1 first using:
  - 3⁴ = 81 (ends in 1)
  - 7⁴ = 2401 (ends in 1)
  - 9² = 81 (ends in 1)
- Then apply Case 1

**Example:** Last 2 digits of **3⁴⁹**
- 3⁴⁸ = (3⁴)¹² = 81¹²
- Last 2 digits of 81¹² → tens digit = (8 × 2) mod 10 = 6, unit = 1 → **61**
- 61 × 3¹ = 61 × 3 = 183 → last 2 digits = **83** ✅

#### Case 3 — Last digit is 2
- 2¹⁰ = 1024 → last 2 digits = **24**
- 24 raised to any power → last 2 digits always **24**
- For 2^odd powers use cyclicity: 2,4,8,6,2,4,8,6...

#### Case 4 — Last digit is 5
- Any power of 5: last 2 digits are always **25** (for powers ≥ 2)
- 5¹ = 05

#### Case 5 — Last digit is 6
- Any power of 6: last 2 digits are always **76** (for powers ≥ 2)
- Wait — actually:
  - 6¹ = 06, 6² = 36, 6³ = 216, 6⁴ = 1296
  - Pattern: 06, 36, 16, 96, 76, 56, 36...
  - Use mod 100 directly for complex cases

> [!TIP]
> For MCQs on last 2 digits, **the most commonly tested bases are 31, 71, 21, 81** (ending in 1) because the formula is clean and direct.

---

## 4. Remainder

### Basic Concept

> **Dividend = Divisor × Quotient + Remainder**
> i.e., `N = D × Q + R` where `0 ≤ R < D`

### Remainder Theorems

#### Remainder of aⁿ ÷ (a-1) = always 1
> Example: 7⁵⁰ ÷ 6 → remainder = **1**

#### Remainder of aⁿ ÷ (a+1)
> - If n is even → remainder = **1**
> - If n is odd → remainder = **a** (which equals divisor - 1)
> Example: 7⁵⁰ ÷ 8 → 50 is even → remainder = **1**
> Example: 7⁵¹ ÷ 8 → 51 is odd → remainder = **7**

### Fermat's Little Theorem (for MCQs)

> If `p` is prime and `a` is not divisible by `p`:
> **aᵖ⁻¹ mod p = 1**

**Example:** Remainder of 2¹⁰⁰ ÷ 7
- p = 7 (prime), p-1 = 6
- 2⁶ mod 7 = 64 mod 7 = 1
- 2¹⁰⁰ = 2⁹⁶ × 2⁴ = (2⁶)¹⁶ × 2⁴
- Remainder = 1¹⁶ × 16 = 16 mod 7 = **2** ✅

### Wilson's Theorem (for MCQs)

> If `p` is prime:
> **(p-1)! mod p = p-1**
> Equivalently: **(p-1)! ≡ -1 (mod p)**

**Example:** Remainder of 6! ÷ 7
- 7 is prime, (7-1)! = 6!
- Remainder = 7-1 = **6** ✅

### Remainder of a Sum / Product

> - Rem[(A + B) / N] = [Rem(A/N) + Rem(B/N)] / N
> - Rem[(A × B) / N] = [Rem(A/N) × Rem(B/N)] / N

**Example:** Remainder of (17 × 23) ÷ 5
- Rem(17/5) = 2, Rem(23/5) = 3
- Rem = (2 × 3) mod 5 = 6 mod 5 = **1** ✅

---

## 5. Divisibility Rules

| Divisor | Rule |
|---|---|
| **2** | Last digit is even (0, 2, 4, 6, 8) |
| **3** | Sum of all digits divisible by 3 |
| **4** | Last **2 digits** divisible by 4 |
| **5** | Last digit is 0 or 5 |
| **6** | Divisible by both **2 and 3** |
| **7** | Double the last digit, subtract from remaining number; repeat till small. If result divisible by 7 → yes |
| **8** | Last **3 digits** divisible by 8 |
| **9** | Sum of all digits divisible by 9 |
| **10** | Last digit is 0 |
| **11** | (Sum of digits at odd positions) − (Sum of digits at even positions) = 0 or divisible by 11 |
| **12** | Divisible by both **3 and 4** |
| **13** | Add 4× last digit to remaining; repeat till small |
| **14** | Divisible by both **2 and 7** |
| **15** | Divisible by both **3 and 5** |
| **16** | Last **4 digits** divisible by 16 |
| **25** | Last **2 digits** divisible by 25 |

### Divisibility by 7 — Example
> Is 1071 divisible by 7?
> 107 − (2×1) = 107 − 2 = 105
> 10 − (2×5) = 10 − 10 = 0 → **Yes** ✅

### Divisibility by 11 — Example
> Is 29,detector 7 → 2olean: Is 39457 divisible by 11?
> Odd positions (1st, 3rd, 5th): 3 + 4 + 7 = 14
> Even positions (2nd, 4th): 9 + 5 = 14
> Difference = 14 − 14 = **0** → Yes ✅

> [!IMPORTANT]
> For divisibility by **6**: number must satisfy BOTH rules for 2 AND 3.
> A number divisible by 6 is always even AND its digit sum is divisible by 3.

---

## 6. Cyclicity

Cyclicity refers to the **repeating pattern** in the unit digits of powers of a number.

| Unit Digit | Cyclicity | Cycle |
|---|---|---|
| 0 | 1 | {0} |
| 1 | 1 | {1} |
| 2 | 4 | {2, 4, 8, 6} |
| 3 | 4 | {3, 9, 7, 1} |
| 4 | 2 | {4, 6} |
| 5 | 1 | {5} |
| 6 | 1 | {6} |
| 7 | 4 | {7, 9, 3, 1} |
| 8 | 4 | {8, 4, 2, 6} |
| 9 | 2 | {9, 1} |

> [!NOTE]
> Digits with cyclicity 1 → 0, 1, 5, 6 → their unit digit **never changes** regardless of power.
> Digits with cyclicity 2 → 4, 9
> Digits with cyclicity 4 → 2, 3, 7, 8

### Cyclicity-Based Shortcut

```
Step 1: Identify unit digit of base
Step 2: Find its cyclicity (C)
Step 3: Divide exponent by C → get remainder R
Step 4: If R = 0 → answer is last element of cycle
        If R ≠ 0 → answer is Rth element of cycle
```

---

## 7. Fast Maths

### Multiplication Tricks

#### Multiplying by 5
> N × 5 = N × 10 / 2 = divide by 2, add zero

**Example:** 346 × 5 = 3460 / 2 = **1730**

#### Multiplying by 9
> N × 9 = N × 10 − N

**Example:** 67 × 9 = 670 − 67 = **603**

#### Multiplying by 11
> Write first and last digit. Middle digits = sum of adjacent pairs.

**Example:** 352 × 11
- First digit: 3
- 3+5 = 8
- 5+2 = 7
- Last digit: 2
- Answer: **3872** ✅

#### Multiplying by 99
> N × 99 = N × 100 − N

**Example:** 47 × 99 = 4700 − 47 = **4653**

#### Squaring Numbers Ending in 5
> (a5)² = a(a+1) | 25

**Example:** 65² = 6×7 | 25 = **4225** ✅

#### Squaring Numbers Close to 100
> (100 ± d)² = (100 ± 2d) | d²

**Example:** 97² = (100-3)² = 94 | 09 = **9409** ✅

#### Vedic Maths — Base Method (Multiplying near a base)
> For numbers near 100:
> (100 - a)(100 - b) = (100 - a - b) | ab

**Example:** 97 × 94
- Deficits: 3, 6
- Cross: 97-6 = 91 (or 94-3 = 91)
- Product of deficits: 3×6 = 18
- Answer: **9118** ✅

### Division Tricks

#### Dividing by 5
> N ÷ 5 = N × 2 / 10 → multiply by 2, then divide by 10

**Example:** 345 ÷ 5 = 690 / 10 = **69**

#### Dividing by 25
> N ÷ 25 = N × 4 / 100

**Example:** 1250 ÷ 25 = 5000 / 100 = **50**

### Squares to Memorize

| n | n² | n | n² |
|---|---|---|---|
| 1 | 1 | 16 | 256 |
| 2 | 4 | 17 | 289 |
| 3 | 9 | 18 | 324 |
| 4 | 16 | 19 | 361 |
| 5 | 25 | 20 | 400 |
| 6 | 36 | 21 | 441 |
| 7 | 49 | 22 | 484 |
| 8 | 64 | 23 | 529 |
| 9 | 81 | 24 | 576 |
| 10 | 100 | 25 | 625 |
| 11 | 121 | 26 | 676 |
| 12 | 144 | 27 | 729 |
| 13 | 169 | 28 | 784 |
| 14 | 196 | 29 | 841 |
| 15 | 225 | 30 | 900 |

### Cubes to Memorize

| n | n³ | n | n³ |
|---|---|---|---|
| 1 | 1 | 6 | 216 |
| 2 | 8 | 7 | 343 |
| 3 | 27 | 8 | 512 |
| 4 | 64 | 9 | 729 |
| 5 | 125 | 10 | 1000 |

### Important Algebraic Identities

| Identity | Formula |
|---|---|
| (a+b)² | a² + 2ab + b² |
| (a-b)² | a² - 2ab + b² |
| a² - b² | (a+b)(a-b) |
| (a+b)³ | a³ + 3a²b + 3ab² + b³ |
| (a-b)³ | a³ - 3a²b + 3ab² - b³ |
| a³ + b³ | (a+b)(a² - ab + b²) |
| a³ - b³ | (a-b)(a² + ab + b²) |
| (a+b+c)² | a²+b²+c²+2ab+2bc+2ca |

---

## 8. Simplification (BODMAS)

**B-O-D-M-A-S** defines the order of operations:

| Letter | Stands For | Operation |
|---|---|---|
| B | Brackets | Solve innermost bracket first: ( ) then { } then [ ] |
| O | Of | Multiplication expressed as "of" (e.g., ½ of 20) |
| D | Division | ÷ |
| M | Multiplication | × |
| A | Addition | + |
| S | Subtraction | − |

> [!IMPORTANT]
> In India exams, **O = Order/Of = powers and roots** as well. Some books show **PEDMAS** (used in US) where P = Parentheses, E = Exponents — same concept different name.

### Bracket Priority (innermost first)
```
( )  →  { }  →  [ ]
```

### Example
> Simplify: 5 + 3 × [2 + {4 × (8 ÷ 2) − 3}]
> = 5 + 3 × [2 + {4 × 4 − 3}]
> = 5 + 3 × [2 + {16 − 3}]
> = 5 + 3 × [2 + 13]
> = 5 + 3 × 15
> = 5 + 45
> = **50** ✅

### Fractions — Key Rules

| Operation | Rule |
|---|---|
| a/b + c/d | (ad + bc) / bd |
| a/b × c/d | ac / bd |
| a/b ÷ c/d | a/b × d/c = ad/bc |
| Complex fractions | Simplify numerator and denominator separately first |

---

## 9. LCM & HCF

### Definitions

| Term | Definition |
|---|---|
| **HCF** (Highest Common Factor) | Largest number that divides all given numbers exactly. Also called GCD (Greatest Common Divisor) |
| **LCM** (Least Common Multiple) | Smallest number that is exactly divisible by all given numbers |

### Key Relationship

> **HCF × LCM = Product of two numbers** *(only for TWO numbers)*
> i.e., HCF(a,b) × LCM(a,b) = a × b

> [!WARNING]
> This formula **only works for exactly 2 numbers**. Do NOT apply it to 3 or more numbers — a very common MCQ trap.

### Methods to Find HCF

#### Method 1 — Prime Factorization
> HCF = Product of **lowest powers** of **common prime factors**

**Example:** HCF of 36 and 48
- 36 = 2² × 3²
- 48 = 2⁴ × 3¹
- HCF = 2² × 3¹ = **12** ✅

#### Method 2 — Division Method (Euclidean Algorithm)
> Divide larger by smaller → remainder becomes new divisor → repeat till remainder = 0 → last divisor = HCF

**Example:** HCF of 48 and 18
- 48 = 18 × 2 + 12
- 18 = 12 × 1 + 6
- 12 = 6 × 2 + 0
- HCF = **6** ✅

### Methods to Find LCM

#### Method 1 — Prime Factorization
> LCM = Product of **highest powers** of **all prime factors** present

**Example:** LCM of 12 and 18
- 12 = 2² × 3¹
- 18 = 2¹ × 3²
- LCM = 2² × 3² = **36** ✅

#### Method 2 — Division Method
> Divide all numbers by a common prime factor simultaneously. Continue until no common factor remains. LCM = product of all divisors used × remaining numbers.

### LCM & HCF — Application Problems

#### Type 1 — Largest number that divides a, b, c leaving remainder r
> HCF of (a-r), (b-r), (c-r)

#### Type 2 — Largest number that divides a, b, c leaving remainders r₁, r₂, r₃
> HCF of (a-r₁), (b-r₂), (c-r₃)

#### Type 3 — Smallest number divisible by a, b, c
> = LCM(a, b, c)

#### Type 4 — Smallest number that when divided by a, b, c leaves remainder r
> = LCM(a, b, c) + r

#### Type 5 — Bells ringing together problem
> If bells ring at intervals of a, b, c seconds — they ring together every **LCM(a,b,c)** seconds

#### Type 6 — Largest tile/square size for a room
> = HCF(length, breadth)

#### Type 7 — Number of tiles required
> = (length × breadth) / (HCF)²

### HCF & LCM of Fractions

| | Formula |
|---|---|
| **HCF of fractions** | HCF of numerators / LCM of denominators |
| **LCM of fractions** | LCM of numerators / HCF of denominators |

**Example:** HCF of 2/3 and 4/9
- HCF of (2, 4) = 2
- LCM of (3, 9) = 9
- HCF = **2/9** ✅

**Example:** LCM of 2/3 and 4/9
- LCM of (2, 4) = 4
- HCF of (3, 9) = 3
- LCM = **4/3** ✅

---

## 📌 Extra Notes

> [!NOTE]
> Everything below goes beyond the core classroom syllabus but is **directly MCQ-relevant** and cross-referenced from RS Aggarwal, M. Tyra, and CAT-level sources.

### 📌 Types of Numbers — Extended

| Type | Definition | Example |
|---|---|---|
| Armstrong Number | Sum of cubes of digits = number itself (3-digit) | 153 = 1³+5³+3³ |
| Perfect Square | Square of an integer | 1, 4, 9, 16, 25... |
| Perfect Cube | Cube of an integer | 1, 8, 27, 64, 125... |
| Palindrome Number | Reads same forwards and backwards | 121, 1331 |
| Automorphic Number | Square ends in the number itself | 5²=25, 6²=36, 25²=625 |
| Narcissistic Number | Sum of digits raised to power of digit count = number | 9474 = 9⁴+4⁴+7⁴+4⁴ |
| Abundant Number | Sum of proper factors > number | 12 (1+2+3+4+6=16>12) |
| Deficient Number | Sum of proper factors < number | 8 (1+2+4=7<8) |

### 📌 Counting Digits and Numbers

| Range | Count of Numbers |
|---|---|
| 1-digit numbers | 9 (1 to 9) |
| 2-digit numbers | 90 (10 to 99) |
| 3-digit numbers | 900 (100 to 999) |
| n-digit numbers | 9 × 10^(n-1) |

**Total digits used from 1 to n:**
- 1 to 9: 9 × 1 = 9 digits
- 1 to 99: 9 + 90×2 = 189 digits
- 1 to 999: 189 + 900×3 = 2889 digits

### 📌 Divisibility — Advanced Rules

| Divisor | Rule |
|---|---|
| **19** | Add 2× last digit to remaining number |
| **17** | Subtract 5× last digit from remaining number |
| **7** | Subtract 2× last digit from remaining number |
| **13** | Add 4× last digit to remaining number |

### 📌 Number of Zeros at End of n!

> Count of trailing zeros in n! = count of times 10 divides n!
> Since 10 = 2 × 5, and factor 5 is always limiting:
> **Zeros = ⌊n/5⌋ + ⌊n/25⌋ + ⌊n/125⌋ + ⌊n/625⌋ + ...**

**Example:** Trailing zeros in 100!
= ⌊100/5⌋ + ⌊100/25⌋ + ⌊100/125⌋
= 20 + 4 + 0 = **24 zeros** ✅

### 📌 Highest Power of Prime p in n!

> **= ⌊n/p⌋ + ⌊n/p²⌋ + ⌊n/p³⌋ + ...**

**Example:** Highest power of 3 in 20!
= ⌊20/3⌋ + ⌊20/9⌋ + ⌊20/27⌋
= 6 + 2 + 0 = **8** ✅

### 📌 Number of Factors

> If N = p^a × q^b × r^c ...
> **Number of factors = (a+1)(b+1)(c+1)...**

**Example:** Factors of 360
- 360 = 2³ × 3² × 5¹
- Factors = (3+1)(2+1)(1+1) = 4×3×2 = **24 factors** ✅

**Sum of factors:**
> = [(p^(a+1) - 1)/(p-1)] × [(q^(b+1) - 1)/(q-1)] × ...

### 📌 Important Number Theory Rules

| Rule | Statement |
|---|---|
| Sum of first n natural numbers | n(n+1)/2 |
| Sum of first n odd numbers | n² |
| Sum of first n even numbers | n(n+1) |
| Sum of squares of first n natural numbers | n(n+1)(2n+1)/6 |
| Sum of cubes of first n natural numbers | [n(n+1)/2]² |

### 📌 Divisibility — Composite Rules

| Number | Break Into |
|---|---|
| 12 | 3 and 4 |
| 15 | 3 and 5 |
| 18 | 2 and 9 |
| 24 | 3 and 8 |
| 36 | 4 and 9 |
| 44 | 4 and 11 |
| 45 | 5 and 9 |
| 48 | 3 and 16 |

> [!NOTE]
> For composite divisibility — always break into **co-prime pairs** (not just any factors). Example: for divisibility by 12, use 3 and 4 (co-prime), NOT 2 and 6 (not co-prime).

### 📌 Remainder — Advanced Patterns

| Expression | Remainder |
|---|---|
| (xⁿ - aⁿ) is always divisible by | (x - a) |
| (xⁿ - aⁿ) when n is even, divisible by | (x + a) also |
| (xⁿ + aⁿ) when n is odd, divisible by | (x + a) |
| n(n+1)(n+2) | Always divisible by 6 |
| n(n+1)(n+2)(n+3) | Always divisible by 24 |

### 📌 HCF & LCM — Trap Questions

> [!WARNING]
> **Trap 1:** HCF is always ≤ LCM. HCF = LCM only when both numbers are equal.
> **Trap 2:** HCF of two consecutive integers is always **1** (they are always co-prime).
> **Trap 3:** LCM of two co-prime numbers = their product.
> **Trap 4:** HCF always divides LCM exactly.

### 📌 BODMAS vs PEMDAS vs PEDMAS

| Acronym | Country | Expansion |
|---|---|---|
| BODMAS | India / UK | Brackets, Of, Division, Multiplication, Addition, Subtraction |
| PEMDAS | USA | Parentheses, Exponents, Multiplication, Division, Addition, Subtraction |
| PEDMAS | USA variant | Same as PEMDAS |
| BIDMAS | UK variant | Brackets, Indices, Division, Multiplication, Addition, Subtraction |

> [!NOTE]
> All are the same rule — just different mnemonics. In Indian exams, **BODMAS** is the standard term.

### 📌 Properties of Remainder

| Property | Statement |
|---|---|
| Negative Remainder | If remainder = -r, then actual remainder = divisor - r |
| Example | Rem(21/5) can be written as -4 ≡ 1 (mod 5) |
| Rem(a/a) | Always 0 |
| Rem(1/a) | Always 1 (when a > 1) |
| Rem[(a × b)/n] | = Rem[Rem(a/n) × Rem(b/n) / n] |

---

## 🔤 Abbreviations Table

| Abbreviation | Full Form | One-line Meaning |
|---|---|---|
| HCF | Highest Common Factor | Largest number dividing all given numbers exactly |
| GCD | Greatest Common Divisor | Same as HCF — used interchangeably |
| LCM | Least Common Multiple | Smallest number divisible by all given numbers |
| BODMAS | Brackets, Of, Division, Multiplication, Addition, Subtraction | Order of operations in simplification |
| N | Natural Numbers | {1, 2, 3, ...} |
| W | Whole Numbers | {0, 1, 2, 3, ...} |
| Z | Integers | {..., -2, -1, 0, 1, 2, ...} |
| Q | Rational Numbers | Numbers expressible as p/q |
| R | Real Numbers | All rational + irrational numbers |
| p/q | Fraction form | p = numerator, q = denominator, q ≠ 0 |

---

## 🧠 Keywords + Concept Map

| Term | Definition | Connected To | Use Case |
|---|---|---|---|
| Unit Digit | Last digit of a number/expression | Cyclicity, Powers | Finding last digit of large exponents |
| Cyclicity | Length of repeating pattern in unit digits | Unit digit, Powers | Shortcut for unit digit problems |
| Remainder | What's left after division | Fermat's Theorem, Wilson's Theorem | Remainder of large powers |
| Divisibility | Whether a number divides another exactly | Factors, Prime numbers | Quick checks without full division |
| HCF | Largest common divisor | LCM, Co-prime | Tiling problems, grouping problems |
| LCM | Smallest common multiple | HCF, Fractions | Bell/timing problems, scheduling |
| BODMAS | Order of operations | Simplification | Solving complex arithmetic expressions |
| Prime Number | Divisible by 1 and itself only | Factorization, HCF, LCM | Foundation of all number theory |
| Co-prime | Two numbers with HCF = 1 | LCM = product | LCM shortcut for co-prime pairs |
| Perfect Number | Proper factors sum = number | Abundant, Deficient | Classification MCQs |
| Trailing Zeros | Zeros at end of n! | Powers of 5 in n! | Factorial-based MCQs |

---

## ⚡ Quick Reference Cheatsheet

### Unit Digit Cyclicity at a Glance

```
Cyclicity 1 → 0, 1, 5, 6     (never changes)
Cyclicity 2 → 4 {4,6}  |  9 {9,1}
Cyclicity 4 → 2 {2,4,8,6}  |  3 {3,9,7,1}  |  7 {7,9,3,1}  |  8 {8,4,2,6}
```

### Remainder Quick Reference

| Scenario | Remainder |
|---|---|
| aⁿ ÷ (a-1) | 1 |
| aⁿ ÷ (a+1), n even | 1 |
| aⁿ ÷ (a+1), n odd | a |
| (p-1)! ÷ p (p prime) | p-1 |
| aᵖ⁻¹ ÷ p (p prime, a not div by p) | 1 |

### LCM & HCF Formula Card

| Scenario | Formula |
|---|---|
| HCF × LCM | = Product of 2 numbers *(only 2 numbers)* |
| HCF of fractions | HCF(num) / LCM(den) |
| LCM of fractions | LCM(num) / HCF(den) |
| Smallest no. leaving remainder r when divided by a,b,c | LCM(a,b,c) + r |
| Largest no. dividing a,b,c leaving same remainder r | HCF(a-r, b-r, c-r) |
| LCM of co-prime numbers a, b | a × b |

### Divisibility — Fast Reference Card

```
÷2  → even last digit
÷3  → digit sum div by 3
÷4  → last 2 digits div by 4
÷5  → ends in 0 or 5
÷6  → div by 2 AND 3
÷8  → last 3 digits div by 8
÷9  → digit sum div by 9
÷10 → ends in 0
÷11 → (odd position sum) - (even position sum) = 0 or 11
÷12 → div by 3 AND 4
÷25 → last 2 digits div by 25
```

### Number of Factors & Zeros

```
Factors of N = pᵃqᵇrᶜ  →  (a+1)(b+1)(c+1)
Trailing zeros in n!    →  ⌊n/5⌋ + ⌊n/25⌋ + ⌊n/125⌋ + ...
Highest power of p in n! → ⌊n/p⌋ + ⌊n/p²⌋ + ⌊n/p³⌋ + ...
```

### Sum Formulas

```
Sum of 1 to n            →  n(n+1)/2
Sum of 1st n odd numbers →  n²
Sum of 1st n even numbers→  n(n+1)
Sum of squares 1 to n    →  n(n+1)(2n+1)/6
Sum of cubes 1 to n      →  [n(n+1)/2]²
```

---

## 🔁 Session Revision Snapshot

### 5-Bullet TL;DR

- ✅ **Unit digit** of any power depends only on the **unit digit of the base** and follows a **cyclicity pattern** (1, 2, or 4)
- ✅ **Last 2 digits** use mod 100 — numbers ending in 1 follow the cleanest formula; others are reduced to base-1 forms
- ✅ **Remainder** of large powers uses Fermat's Little Theorem (for primes) and the (a±1) trick for quick MCQ solving
- ✅ **HCF × LCM = product of two numbers** — this formula is valid **only for exactly 2 numbers**, not 3 or more
- ✅ **BODMAS** governs simplification order — always resolve innermost brackets first, powers before multiplication, division before addition

### MCQ-Likely Concepts — High Priority

| Concept | Why It's Exam-Likely |
|---|---|
| Unit digit of 7^(large power) | Most frequently tested base in exams |
| Trailing zeros in 100! | Classic factorial MCQ |
| HCF × LCM trap for 3 numbers | Trap question — formula doesn't apply |
| Number of factors formula | Appears in nearly every aptitude exam |
| Divisibility by 11 | Needs careful position counting — trap-prone |
| Remainder of aⁿ ÷ (a+1) odd/even rule | Clean 2-second shortcut |
| LCM of fractions | Numerator/denominator swap is a common trap |
| BODMAS with nested brackets | Must know bracket priority order |
| 1 is neither prime nor composite | Standard definitional MCQ |
| Wilson's Theorem | Less-known → appears in advanced sets |

---

<details>
<summary>🧪 Lab / Practice Section</summary>

### Practice Problems — Attempt Before Checking Answers

1. Find the unit digit of 3²⁴⁵ × 7¹³⁸
2. Find the last 2 digits of 41⁴³
3. What is the remainder when 2⁵⁸ is divided by 7?
4. Is 7,469,135 divisible by 11?
5. Find the HCF and LCM of 72, 108, 180
6. Find the number of trailing zeros in 150!
7. How many factors does 720 have?
8. Find the smallest number which when divided by 12, 18, 21 leaves remainder 5
9. Find the unit digit of (1! + 2! + 3! + ... + 100!)
10. Find the HCF of 3/4 and 5/6

<details>
<summary>✅ Answers</summary>

1. Unit digit of 3²⁴⁵ → cycle(3): 3,9,7,1 → 245 mod 4 = 1 → **3**; Unit digit of 7¹³⁸ → cycle(7): 7,9,3,1 → 138 mod 4 = 2 → **9**; Product unit digit = 3×9=27 → **7**
2. 41 ends in 1 → tens digit = (4 × 3) mod 10 = 12 mod 10 = 2 → last 2 digits = **21**
3. Fermat: 2⁶ mod 7 = 1 → 2⁵⁸ = 2⁵⁴ × 2⁴ = (2⁶)⁹ × 16 → 1 × 16 mod 7 = 16 mod 7 = **2**
4. Odd positions (1,3,5,7): 7+6+1+5 = 19; Even positions (2,4,6): 4+9+3 = 16; 19-16 = 3 ≠ 0 or 11 → **Not divisible**
5. 72=2³×3², 108=2²×3³, 180=2²×3²×5; HCF=2²×3²=**36**; LCM=2³×3³×5=**1080**
6. ⌊150/5⌋+⌊150/25⌋+⌊150/125⌋ = 30+6+1 = **37**
7. 720=2⁴×3²×5¹; Factors=(4+1)(2+1)(1+1)=5×3×2=**30**
8. LCM(12,18,21)=252; Answer=252+5=**257**
9. From 5! onwards, all factorials end in 0. So only 1!+2!+3!+4! matter: 1+2+6+24=33; unit digit = **3**
10. HCF(3,5)=1; LCM(4,6)=12; HCF = **1/12**

</details>
</details>

---