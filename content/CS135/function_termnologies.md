---
title: "Before we begin designing programs"
date: 2020-09-10T20:46:19+08:00
slug: "function-terminologies"
description: "Some things to know before writing programs"
keywords: ["CS135", "Waterloo", "functions"]
draft: false
tags: ["CS135", "Waterloo"]
math: true
toc: true
---

Imperative based on frequent changes to the data.

Functional based on computation of new values instead of changing old ones. It is also more self contained and closer related to mathematics.

## Some Terminologies

* Value: Numbers and mathematical objects
* Expressions: Combination of values with functions.
* Functions: Generalized similar expressions.

## Functions

A function is really three parts:

* Name (e.g. $g$)
* Parameters(e.g. $$ ,$y$)
* An algebraic expression using the parameters. (e.g. $x + y$)

When applying functions, **arguments** are taken in as **parameters**.

The function is then evaluated to yield values.

$$\begin{aligned}g(x) &= 2(x) \\g(4) &= 2(4) \\&= 8 \end{aligned}$$

As functions get more complicated, there becomes multiple ways of evaluating the function. That is where the canonical forms comes into play.

## Canonical Forms

The canonical form refers to a natural unique representation of an object, or a preferred notation for some object.

There are two rules:

* Functions are only applied to values (i.e. only apply a function when its parameters // arguments are values)
* If there are multiple substitution, then the left most expression is substituted first.

Going of the first rule, it can also be seen that the basic operators: $+, - \times, \div, \%$ can be seen as functions.

### Harmonizing the parenthesis

Parenthesis does two things currently:

* Specify order of operation: $(2 + 3) \times (4 + 5)$
* Allow functions to be applied to some arguments: $f(2, 3)$

By moving the operators out, we can treat operations as functions:

$$ +(5, 3) = 8$$

## Identifiers and Scope

So far, we have seen how we use algebraic terms to define both the parameters of a function and the function itself.

Algebraic terms can also be used to define constants. Constants are useful because they give meaningful names that does two things:

* Make things easier to read
* Make changing the values associated with the constant easier (You only need to change in one location)

Collectively, these algebraic terms can be called identifiers.

Identifiers have scope.  Scope refers the area in which the identifier is valid and has an effect.

There is two broad types of scope:

* Global: Refers to the range of the whole program
* Local: Refers the the range within a set of braces

Often, the smallest enclosing scope has priority. (This can be overridden)

In functional programming languages duplicate identifiers within the same scope will cause errors.
