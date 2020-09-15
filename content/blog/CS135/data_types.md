---
title: "Data Types"
date: 2020-09-15T15:31:12+08:00
slug: "data-types"
description: "Different types of data introduced"
keywords: ["CS135", "Waterloo", "data types", "DrRacket"]
draft: false
tags: ["CS135","DrRacket", "Waterloo"]
math: true
toc: true
---

Recall from the introduction that [values](../CS135/function_termnologies.md) are just an instance of a type of data.

The literal is the way you write something down.  
Literals of `Bool` are `True` and `False`.

DrRacket also have `symbols` (single quote before name) and `strings` (double quote), Character (smallest component of a string).

## Symbols

Symbols are really like the `Enumerate` type in other languages, they are limited in functionality and cannot have certain characters like spaces

It is normally used when a small set of labels is need and no functionality required other than comparing equality.

Otherwise, consider using a string.

## String

Strings tend to have a fair bit of built in functions regardless of the language of choice.

Strings are really compound data (sequence of characters)

## Boolean

The term Boolean comes from the name of the British mathematician George Boole, who defined an algebra on these values.

A `Boolean` can take on two different kinds of value `True` and `False`.

## Predicates

Predicates are functions that produce a boolean result.

Comparisons are a type of predicate since it consumes two values and produce a boolean value.

Combined with logical operators `and`, `or`, and `not` complex predicates can be built.

In many languages, short circuiting occurs where the program only evaluates as much as it needs to reach a conclusion.  
This can be taken advantage of to by putting complex checks last.

Some interesting predicates in DrRacket includes:

- `string>=?` compares string to one another
- `equal?` checks if two values are equal
- `=` only applies to numbers as with all the other `> < <= etc` operators

## Conditional Expressions

Conditional Expressions are used make decisions.

This is done by stacking predicates one after another.

In DrRackets, `cond` is used and at least one conditions **must** evaluate to `true`. (you can just at an `else` for safety measure.)

``` racket
(define (foo x)
  (cond [(even? x) 0]
        [(= x 2) 2]
        [(not (even? x)) 1]
        [else 999]))
```

Conditional expressions can be simplified on the notion that if it is being asked, all previous predicates have evaluated to false.

### Testing conditional expressions

Testing Conditional expressions should be simple and direct aimed at:

- Boundary conditions should be tested explicitly (if pass if 50 and above, a test should include what happens at 50)
- There should be at least 1 test for each possible case.

## Testing Logic operators

Test for `and`:

- One test for **each clause** to make it `False`
- One test to make **all the clauses** `True`

Test for `or`:

- One test for **each clause** to make it `True`
- One test to make **all the clauses** `False`

Notice the subtle distinction between `and` and `or`.
