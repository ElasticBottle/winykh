---
title: "Divisibility of integers"
date: 2020-09-30T15:30:19+08:00
slug: "divisibility-of-integers"
description: "An introduction to Mathematical Proofs"
keywords: ["MATH135", "Waterloo", "divisibility of integers", "Proofs"]
draft: false
tags: ["MATH135", "Waterloo"]
math: true
toc: true
---

Divisibility of integers is a tricky topics after all, when we divide two integers $a$ and $b$, we are not guaranteed to get back an integer.

### Notations on Divisibility

When $a$ is a **factor** of $b$, we write $a \mid b$. This means that $\exists k \in \mathbb{Z} s.t. b = ka$

In other words, $b$ is **divisible by** $a$, or $b$ is a **multiple** of $a$, or $a$ is the **divisor** of $b$.

It's like the opposite of how we write divide. $4/2$ gets written as $2\mid4$. (\mid is NOT dividing. It merely gives us information about the Divisibility of one number by another.)

When a $b$ is not divisible by $a$, we write $a \nmid b$.

Rules of divisibility:

- For all integers $a$, $a \mid 0$ since $0 = 0 \times a$. In particular, $0 \times 0$ is true
- For alll integers $a$, $0 \nmid a$, since there is no integer $k$ such that $0 \times k = a$.
- For all integers $b$, $1 \mid b$, since $b$ can be written as $1 \times b = b$. $-1 \mid b$ as well because $b = (-b) \times (-1)$.

### Transitivity of divisibility

The transitivity of divisibility states that for all integers $a, b, c$, if $a\mid b$ and $b\mid c$, then $a\mid c$

Proof:

$$\begin{aligned}&\text{Since } a\mid b, \text{this means that there exist } r\in \mathbb{Z}, \ni b = ra\\&\text{Similarly, since } b \mid c, \exists t \in \mathbb{Z} \ni c = tb \\ & \text{Subbing } ra \text{ as } b, \text{ we get } c = t(ra) = (tr)a\\&\text{Since } r \text{ and } a \text{ are integers, from the definition of divisibility, } a\mid c\end{aligned}$$

### Divisibility of Integer Combinations

The divisibility of integer combination states that $\forall a, b, c \in \mathbb{Z}$, if $a\mid b$ and $a \mid c$, then for all integers $x, y$, $a \mid (xb + yc)$.

Proof:

Let $a, b, c$ be integers and assume $a\mid b$ and $a \mid c$ to be true.

Since $a\mid b$ and $a \mid c$, then $c = ra, b = ta, r,t, \in \mathbb{Z}$.

Let $x, y$ be arbitrary integers, then $(xb + yc)$ is also an integer using known facts about the product and sum of integers.

Using the assumptions,
$$\begin{aligned}xb + yc &= x(ra) + y(ta) \\ &=xra + yta \\&=a(xr + yt)\end{aligned}$$

Since $x, t, y, r \in \mathbb{Z}$, $(xr + yt)$ is also an integer, then by the definition of divisibility, $a \mid (xb + yc)$.
