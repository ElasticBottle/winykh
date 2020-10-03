---
title: "Recursing on various things"
date: 2020-10-1T15:40:12+08:00
slug: "recursion-racket"
description: "Recursing on various recursive data definitions"
keywords: ["CS135", "Waterloo", "recursion","lists", "DrRacket"]
draft: false
tags: ["CS135", "Waterloo"]
math: true
toc: true
---

Let's talk about sorting lists.

## Insertion sort

The easiest of sorts defined recursively.

```racket
;; sort: (listof Num) -> (listof Num)
(define (sort list)
    (cond
        [(empty? list) empty]
        [else (insert (first list)
                      (sort (rest list)))]))

;; insert: Num (listof Num) -> (listof Num)
(define (insert num slon)
    (cond
        [(empty? slon) (cons num empty)]
        [(<= n (first slon)) (cons n slon)]
        [else (cons (first slon) (insert n (rest slon)))]))
```

This allows us to sort a list of numbers in ascending order.

We simply have to flip the `<=` on the second last line to `>=` for descending order.

## List Abbreviation

Instead of initializing a fixed length list with `cons` all the time, we can write `(list 1 2 3 4 5)`.

## Different kinds of list

There are many different types of list

1. Flat lists
2. List of List
3. Nested List (List containing list containing list...)

## Association List: Dictionaries

Dictionaries are mapping of one kind of value to another.

An association list is basically a `(listof (list (anyof Str Num Symb) Any))`, where the first value has to be unique.

```racket
;; An Association List (AL) is one of:
;; * empty
;; * (cons (list Nat Str) AL)
;;     Requires key(Nat) to be unique

;; (AL-template): PURPOSE
;; Examples:
(check-expect (AL-template empty) ...)
(check-expect (AL-template (list (list 1 "item"))) ...)

;; AL-template: AL -> Any
(define (AL-template al)
    (cond
        [(empty? al) ...]
        [(cons? al) (... (kv-template (first al)) ...
                    ... (AL-template (rest al)) ...)]))

;; (kv-template kv): PURPOSE
;; Examples:
(check-expect (kv-template ) ...)
(check-expect (kv-template ) ...)

;; kv-template: (list Nat Str) -> Any
(define (kv-template kv)
    (... (first kv)
    ... (second kv)...))
```

## Processing Two Lists

Processing two list at once can get quite complicated.

Really though, there is only three cases to consider

1. One of the list is just going along for the ride.
2. Both the list are the same length and one item from each list is processed each time
3. Unequal lengths, process one or both cases.

The first case is the same as processing a single list.

The second case is more involved. The only difference however, is that we process two things instead of one before making the recursive call.

```racket
;; (lockstep-template lst1 lst2): PURPOSE
;; Examples:
(check-expect (lockstep-template empty empty) ...)
(check-expect (lockstep-template (list 1) (list 1)) ...)
(check-expect (lockstep-template (list 1 2) (list 1 2)) ...)

;; lockstep-template: (listof X) (listof Y) -> Any
;;  Requires: (length X) = (length Y)
(define (lockstep-template lst1 lst2)
    (cond
        [(empty? lst1) ...]
        [else (... (first lst1) ... (first lst2) ...
                (lockstep-template (rest lst1) (rest lst2)) ...)]))

```

For the third case we have four cases to consider:

1. Both list are empty
2. `List1` empty, `list2` not empty
3. `list2` empty, `list1` not empty
4. Both list are not empty

Interestingly enough, there are often some interesting speed ups that we can do _after_ implementing the base code consisting of the four cases above.

Do not optimise your code prematurely!

## Processing Multiple Items

In general, the strategy that follows from processing multiple items with recursive data definitions si as follows:

1. Consider each of the possible cases for each data type
2. Ensure that every case is paired with every other case for the other data types

To illustrate, consider natural numbers.

If we were to recurse on a natural numbers and a list. The natural number that can either be 0 or non zero and the list is either empty or not empty.

As such, we would have 4 different cases.

1. `empty`, `zero`
2. `empty`, `not zero`
3. `not empty`, `zero`
4. `not empty`, `not zero`
