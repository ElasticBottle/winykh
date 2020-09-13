---
title: "The Design Recipe"
date: 2020-09-10T20:46:19+08:00
slug: "design-recipe"
description: "How to design a good function"
keywords: ["CS135", "Waterloo", "functions", "design recipe"]
draft: false
tags: ["CS135", "Waterloo"]
math: true
toc: true
---

Just like how the best food is distilled down from an art to a science where everyone can follow along, so too is designing functions.

Now everyone can write delicious an yummy functions!

## Ingredients for design recipe

* Purpose: Describes what the function is to compute.
* Contract: Describes what type of arguments the function consumes and wha ttype of value it produces.  
* Examples: Illustrating the typical use of the function.
* Definition: The Racket definition of the function (header&body).
* Tests: A representative set of function applications and their expected values.Examples also serve as Tests.

## Preparing the Function

1. Draft the purpose of the function
2. Write examples to show what the function will do.
3. Establish the contract and define the header
4. Finalize purpose with parameter names
5. Finish defining the body.
6. Write the test.

Lets look at it in closer detail.

## Drafting the Purpose

This is probably the simplest yet most important part.

Simply write about ***what*** the program (function) will do.

```python
# sum numbers together
```

## Write the examples

This has three parts:

* The syntactically correct definition for how the functions should be used
* An expected value from the above function call
* A walk-through on how the value was arrived at

```python
# 1 + 2 + 3 + 4 = 10 This is the walk-through
>>> assert sum(1, 2, 3, 4) # This shows how the function is used
10 # The expected value
```

## Establish the contract and write the header

There is two parts here:

1. The contract should specify what type of value goes in and what type of value comes out of the functions
   1. The incoming type should be as general as possible.
   2. The outgoing type should be as specific as possible.
   3. Contract should also specify any other requirement on the parameters
2. The header should define the name and the arguments that the function takes.

```python
# sum_all: List[Union[int, float]] -> int
def sum_all(*args):
    pass
```

### Contract enforcement

Contracts are important. They essentially specify what the function will or will not do.

As such, it is important to get it right.

For languages like python, ,Js, racket, where things are dynamically typed, it is hard to enforce these contracts.

ON the contrary, static typed program makes it easy to ensure that arguments are of the right type.

Dynamically typed languages often have their own static typed systems when developing for larger programs.

## Finish the purpose

At this stage everything should have fell into place and all that is left is to finish what we started.

```python
# sum_all(*args takes in any number of argument and sums them up
```

## Finish the Body

```python
def sum_all(*args):
    return sum(*args)
```

## Write the test

The last step in the design recipe process is to write additional tests to cover any complexities not covered by the examples.

```python
# Trivial example
assert sum_all(-1, 1) == 0
```

A small note, answers to test should be calculated independently. You should not be using your program to derive the answer.

## Examples Versus Tests

Both show what is expected given a certain input

Examples, however, focuses more on how the function is mean to be used. Does not actually take into account how the function was implemented.

Test, on the other hand, focus more the edge-cases and takes into account how the function was implemented to account for what can go wrong
