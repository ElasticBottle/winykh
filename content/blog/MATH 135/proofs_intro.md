---
title: "Introduction to statements and sets"
date: 2020-09-11T21:19:19+08:00
slug: "intro-proofs"
description: "A short introduction on how to make a true statement"
keywords: ["MATH135", "Waterloo", "Proofs"]
draft: false
tags: ["MATH135", "Waterloo"]
math: true
toc: true
---

- Direct proof
- proof by contrapositive
- proof by contradiction
- proof by induction

## Set

A set is a well-defined, unordered collection of distinct objects.

Each object that appears in this collection is called an element (or member) of the set.

Sets can contain any type of object.

### Some examples of sets

$$\begin{aligned} \mathbb{R} &\text{: real numbers} \\ \natnums &\text{: Natural Numbers, whole numbers from }0 \\ \mathbb{Z} &\text{: Integers} \\ \mathbb{Q} &\text{: Rational Numbers}\end{aligned}$$

We use capital letter sot represent a set, $S$, and small letters to represent elements of a set, $s$.

$\in$ to denote membership, $\notin$ to denote non-membership.

## Statements

A statement is a sentence that has a definite state of being **either true or false**.

### Examples of Statements

$$\begin{aligned}2 + 3 &= 5 \text{ False} \\ \pi + 2 &\leq 5 \text{ True}\end{aligned}$$

We can negate statements, $\neg{A}$.

Double negation brings us back to the start. Or in Math speak, logically equivalent.

$$\neg(\neg{A}) \equiv A \text{ (Note the tripe equal sign)}$$

## Quantified statements

A quantified statement contains four parts:

- A quantifier (universal $\forall$, or existential $\exists$)
- A variable (any symbol representing a quantity or mathematical object),
- A domain (any set)
- An open sentence involving the variable (that is either true or false whenever a value of the variable chosen from the domain is specified).

One example is:

$$\forall{n} \geq 5, n^2 + 2n \leq 20n$$

The first part of the sentence contains the quantifier $\forall$, the variable $n$, and the domain $s \in \{5, 6, ,7, \ldots\}$.

The second part of the statement contains the open sentence $n^2 + 2n \leq 20n$. An open sentence simply means that the statement depends on some variables and the truth of the statement cannot be determined.

### Describing statements

Universal Quantified statements:
$$\forall x \in S, P(x)$$
In English: For all $x$ in $S$, $P(x)$ is true. False otherwise.

Existential Quantified statements:
$$\exist x \in S, P(x)$$
In English: There exist at least one value of $x$ in $S$ such that $P(x)$ is true.

## Negating Statements  

| Quantified Statement   | True                                          | False                                           |
| ---------------------- | --------------------------------------------- | ----------------------------------------------- |
| $\forall x\in S, P(x)$ | When $P(x)$ is true for every $x\in S$        | when $P(x)$ is false for at least one $x \in S$ |
| $\exist x \in s, P(x)$ | When $P(x)$ is true for at least one $x\in S$ | When $P(x)$ is false for every $x\in S$         |

Negating Universal Quantified Statements
$$\neg (\forall x\in S, P(x)) \equiv \exist x \in S, \neg (P(x))$$

Negating Existential Quantified Statements
$$\neg (\exist x\in S, P(x)) \equiv \forall x \in S, \neg (P(x))$$

## Multiple quantifiers

Quantifiers in a statement containing more than one quantifier are called nested quantifiers.

The order in which they appear will change the meaning of these statements.

### For all first, then exist

$$\forall x \in X, \exist y \in Y, x > y$$
The quantified statement above is true since we are choosing a single y value after the set $X$ has been establish.

Therefore as long as $y$ is $\min{(X)} - 1$, the above statement will always be true.

### Exist first, then for all

$$\exist x \in X, \forall y \in Y, x > y$$
The above statement is now false because regardless off what $x$ value we choose, there is always a value that $y$ can choose such that $y>x$.

Going one step further
$$\forall x \in X, \exist y \in Y, x > y \not\equiv \exist x \in X, \forall y \in Y, x > y$$

The open statement $x > y$ can also be replaced with $Q(x, y)$ to mean an open set whose truth value can be determine for $x$ and $y$, chosen from the domain $X$, and $Y$ respectively

### More than 2 quantifiers

Consider:

$$\forall x \in X, \exist y \in Y, \forall z \in Z, R(x, y, z)$$

This statement can be rewritten as:

$$\left.\begin{aligned} &\forall x \in X, P(X) \\ \text{where }P(X) \text{ is } &\exist y \in Y, Q(x,y) \\ \text{where } Q(x,y) \text{ is } &\forall z \in Z, R(x,y,z)\end{aligned}\right\rbrace$$

Notice the nesting.

Such a scenario is especially common in deriving limits for calculus.

#### Limits in calculus

The limit, $L$, in calculus is defined such that as $x$ approaches $a\in \mathbb{R}$, $f(x)$ tends towards $L$.

More formally, for any positive tolerance, $\epsilon$, from $L$, there exist a $\delta \gt 0$, such that if $|x - a|\lt \delta$ is true, then $|f(x) - L| \lt \epsilon$.

Even more formally, $\forall \epsilon \in \mathbb{R}, \exist \delta \in \mathbb{R}, \forall x \in \mathbb{R}, if |x - a|\lt \delta, then |f(x) -L| < \epsilon$

## Negating Multiple Quantifiers

Negating quantifiers is simply a matter of working from right to left and doing one of the following:

- Changing $\forall$ into $\exist$ or vice versa
- Changing the open statement to the opposite, $= \text{ becomes } \neq, \lt \text{ becomes } \geq$
