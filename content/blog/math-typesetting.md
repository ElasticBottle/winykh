---
title: "Math Typesetting"
date: 2020-06-05
slug: "math-typesetting"
description: "A brief guide to setup KaTeX"
keywords: ["gohugo", "hugo", "go", "blog"]
draft: false
tags: ["math"]
math: true
toc: false
---

Mathematical notation in a Hugo project can be enabled by using third party JavaScript libraries.
<!--more-->

In this example we will be using [KaTeX](https://katex.org/)

- Create a partial under `/layouts/partials/math.html`
- Within this partial reference the [Auto-render Extension](https://katex.org/docs/autorender.html) or host these scripts locally.
- Include the partial in your templates like so:  

```
{{ if or .Params.math .Site.Params.math }}
{{ partial "math.html" . }}
{{ end }}
```  
- To enable KaTex globally set the parameter `math` to `true` in a project's configuration
- To enable KaTex on a per page basis include the parameter `math: true` in content files.

**Note:** Use the online reference of [Supported TeX Functions](https://katex.org/docs/supported.html)


### Examples

Inline math: $$ \varphi = \dfrac{1+\sqrt5}{2}= 1.6180339887… $$

Block math:

$$
\sigma(t) = \cfrac{1}{1 + e^{-t}}
$$
