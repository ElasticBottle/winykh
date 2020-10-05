---
title: "Patterns of Recursion"
date: 2020-10-3T22:06:12+08:00
slug: "patterns-of-recursion"
description: "Understanding the different patterns of recursion"
keywords: ["CS135", "Waterloo", "recursion","patterns of recursion", "DrRacket"]
draft: false
tags: ["CS135", "Waterloo"]
math: true
toc: true
---

We have defined [simple recursion](../CS135/data_definitions_templates.md/#simple-recursion) before.

Aside from needing a base case, simple recursion has two requirements:

1. Arguments are passed into the function unchanged
2. Arguments are one step closer to the base case

Aside from that, there are two other kinds of recursion, accumulative and generative.

## Accumulative Recursion

Accumulative recursion keeps track of a value that stores the information that encompasses everything that the function has seen thus far.

THe accumulated value is then returned when the recursive function reaches a base case.

This accumulated value is known as an accumulator.

Wrappers are often used around accumulated recursion due to the extra parameters that needs to be passed into the function.

Indicators of a accumulative recursion pattern:

* The value(s) in the accumulator function is used in one or more base case.
* There is a wrapper function that sets the initial value of the accumulator.
* All arguments to the recursive function is either:
  * Unchanged
  * One step closer to the base case
  * A partial answer for the evaluated cases thus far.

Often, accumulative recursion can be used to substitute a simple recursion to remove a particular function call in order to speed it up.

Of course, do not pre-maturely optimize!

## Generative Recursion

In generative recursion, the parameters for the recursion function is freely calculated at each step.

There are no constraints about what can and cannot be passed as an argument, unlike simple and accumulative recursion.

Euclid's greatest common divisor is an example of a simple generative recursion algorithm.
