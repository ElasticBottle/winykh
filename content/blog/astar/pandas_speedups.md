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
# Faster, avg time taken 0.616 sec
pd.read_csv(file_path, dtype={‘a’: np.float64, ‘b’: np.int32, ‘c’: 'string'})
# Slower, avg time taken 0.581 sec
pd.read_csv(file_path)

# Test was done by loading a 160,000 line csv file with int, strings, and floats.
# Repeated and averaged after 100 times.
```

Note that even though the read_csv function is actually slower by about 3ms.

Time savings come from later on. We no longer have to convert rows to a specific type since it is already done.

Converting one row of `int` to `string` in my use case took upwards of a second a row.

For conversion of time, there can be huge time savings as noted by [this stackOverflow answer](https://stackoverflow.com/questions/32034689/why-is-pandas-to-datetime-slow-for-non-standard-time-format-such-as-2014-12-31).

Be as explicit as possible in the datetime format.

```python
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

If `pd.eval()` is not an option, then using python's built in `map` or `list comprehensions` will be the next best things.

Also, `np.vectorize` or `np.frompyfunc` (`np.vectorize` wraps this function) are alternatives to consider. While it has been noted that they are merely convenience functions, they seem to speed up certain task in my testing.

Again, your mileage may vary.

Benchmarks for your use case are the only way to know for sure.

One thing to take note is that you should avoid premature optimization!

Finally, `eval()` should only be used when your datasets is > 15,000 or so entries

For more on `eval()` and `query()`, check out [the docs](https://pandas.pydata.org/pandas-docs/version/0.22/enhancingperf.html#enhancingperf-eval).

For `np.vectorize()`. Docs [here](https://numpy.org/doc/stable/reference/generated/numpy.vectorize.html)
