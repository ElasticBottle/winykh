---
title: "Going Faster with Pandas in Python"
date: 2020-10-27T16:52:23+08:00
slug: "speeding-up-pandas-in-python"
description: "Making pandas go whoosh"
keywords: ["Pandas", "Data Manipulation", "Data Processing", "optimization", "python"]
draft: false
tags: ["aStar", "pandas", "optimization"]
math: false
toc: true
---

A short guide for tricks to speed up pandas in everyday scenario.

## Be Explicit

!#@^$@^!&. That's the feeling when things take too long and come out wrong.

With Pandas, being explicit helps.

Especially when importing datasets or when converting `Object` into `datetime`.

```python
## importing things
# Faster
pd.read_csv(file_path, dtype={‘a’: np.float64, ‘b’: np.int32, ‘c’: str})
# Slower
pd.read_csv(file_path)

## Converting things
# faster
pd.to_datetime(df[column_name], format='%d/%m/%y %H:%M')

# slower
pd.to_datetime(df[column_name])
```

## Avoid Looping

Looping is slow.

Common methods used include:

* `for i in df.iterrows()`
* `for i in df.itertuples()`
  * This tend to be a little faster than `iterrows()`

The worst you could do is `for i in range(len(df))` followed by `iloc` chained accessors.

## Functional is slightly better

We cold use `.apply`

```python
df.apply(lambda row: do_something(row), axis = 1)
# 1 specifies taking all the columns at once, so operation is row-wise
```

This is slightly better than our iterative style, but we can do even better.

## Vectorize whenever possible

```python
result2 = df.eval('@myfunc(A + @variable)')
```

`pd.eval()` can also be used, but we lose the ability to call functions and variables with the `@`.

If functions and variables are not required, `pd.eval()` should be used since `df.eval()` [simply calls `pd.eval()` with some overhead.](https://stackoverflow.com/questions/38725355/when-to-use-dataframe-eval-versus-pandas-eval-or-python-eval)

One thing to take note is that you should avoid premature optimization!

Basic python methods are still faster when dealing with smaller datasets (< 15,000)

For more on `eval()` and `query()`, check out [the docs](https://pandas.pydata.org/pandas-docs/version/0.22/enhancingperf.html#enhancingperf-eval).

Works well with `np.vectorize()`. Docs [here](https://numpy.org/doc/stable/reference/generated/numpy.vectorize.html)
