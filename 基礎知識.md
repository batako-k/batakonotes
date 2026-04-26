# Finite Fields for KZG Commitments

## Overview

This document builds a rigorous understanding of finite fields as a foundation for KZG commitments and modern cryptography.

---

## 1. What is a Field?

A field (F) is a set equipped with two operations (addition and multiplication) such that:

### Addition

* Closure: (a + b \in F)
* Associativity: ((a+b)+c = a+(b+c))
* Identity: (0) such that (a+0=a)
* Inverse: (\forall a, \exists -a)

### Multiplication (excluding 0)

* Closure: (a \cdot b \in F)
* Associativity: ((ab)c = a(bc))
* Identity: (1 \neq 0)
* Inverse: (\forall a \neq 0, \exists a^{-1})

### Distributive Law

[
a(b+c) = ab + ac
]

---

## 2. Finite Fields

A finite field is a field with finitely many elements.

### Key Theorem

Every finite field has size:
[
p^n
]
where (p) is a prime number.

---

## 3. Prime Fields (\mathbb{F}_p)

Defined as:
[
\mathbb{F}_p = {0,1,2,...,p-1}
]
with arithmetic modulo (p).

### Example (mod 7)

[
5 + 4 \equiv 2 \mod 7
]
[
3 \cdot 5 \equiv 1 \mod 7
]

### Multiplicative Inverse

Find (a^{-1}) such that:
[
a \cdot a^{-1} \equiv 1 \mod p
]

---

## 4. Why Prime Modulus Matters

If modulus is not prime, inverses may not exist.

Example (mod 8):
[
2 \cdot 4 \equiv 0
]

This introduces zero divisors → not a field.

---

## 5. Extension Fields (\mathbb{F}_{p^n})

Constructed as:
[
\mathbb{F}_p[x] / (f(x))
]
where (f(x)) is an irreducible polynomial.

### Example Structure

Elements look like:
[
a + bx
]

with reduction rule (example):
[
x^2 = -1
]

---

## 6. Irreducible Polynomials

An irreducible polynomial cannot be factored over (\mathbb{F}_p).

They play the role of “prime numbers” in polynomial rings.

---

## 7. Key Properties

### 7.1 Multiplicative Group

[
\mathbb{F}_p^\times
]
is cyclic.

### 7.2 Fermat’s Little Theorem

[
a^{p-1} \equiv 1 \mod p
]

### 7.3 Frobenius Map

[
a^{p^n} = a
]

---

## 8. Connection to KZG Commitments

Finite fields enable:

* Polynomial arithmetic
* Division: ((f(s) - y)/(s - z))
* Well-defined evaluation

These are essential for polynomial commitments.

---

## 9. Future Extensions

Planned additions:

* Polynomial division in finite fields
* Lagrange interpolation
* FFT over finite fields
* Elliptic curves over finite fields
* Pairings and bilinearity

---

## Notes

This document is a living note. Content will be expanded as understanding deepens.
maybe
