---
title: "Word Embeddings"
date: 2020-07-16T22:25:14+08:00
slug: "word-embeddings"
description: "Everything about word embeddings"
keywords: ["Word embeddings", "word vectors"]
draft: true
tags: ["FastAI", "AI"]
math: false
toc: false
---


Word Embeddings are nothing more than a collections of word vectors.

Then what are word vectors?

They are simply a way in which a vector can represent a word.

Often this vector is tens or hundred of dimension big.

![a word vector](/images/fastai/word_vector.png "A word vector")

This is juxtaposed to a one-hot encoded matrix where a vector the same length of the vocabulary is created. Each word then occupy a single spot in that vector.

The advantages are numerous:

- Semantic capturing
  - Meaningful spatial representation
  - Words similar to each other are closer to each other in vector space
- Better use of memory
  - Much smaller than 1 hot encoded vectors

The downsides:

- Takes more time to create (more soon)

## Creating word embeddings

### Continuous bag of word model

This uses surrounding words as a context $\plusmn x$ where $x$ is a parameter to tune.

Each of the surrounding word is converted into ao one hot encoded matrix.

This matrix is then fed into a weight matrix which will compute an output vector representing the word.

### Skip Grams

The target word is used to compute the surrounding words.
