---
layout: post
date:   2022-01-19
categories: [programming]
comment: true
---

# Python Array Initialization

Sometimes, we need to initialize an array with a fixed size. Let's say we want an array of size `n`.
In python, instead of the canonical list.append() method, there are some less beautiful, but useful tricks.

## One-dimensional Arrays
First, let's look at one-dimensional arrays.

There are two common techniques.

Technique *one* looks very clean.
```python
arr1d = [None] * n
```

In python, multiply a list with an integer `n` will return a list of elements copied (not deep copy, as we will discuss later).

Technique *two* looks a more verbose.
```python
arr1d = [None for _ in range(n)]
```

This is a simple list comprehension.

## Two-dimensional Arrays

Now, we would like an empty array of size (n,m)

In case of two-dimensional arrays, technique *one* shown above stops working, while technique *two* continues to work.

Let's look at the working technique first.
```python
arr2d = [[None for _ in range(m)] for _ in range(n)]
```

However, doing the following stops working:
```python
arr2d_wrong = [[None] * m] * n
```

The main concern is what is multiplied with `n`? The answer is a list of list.
Now the inner list becomes the element being copied, shallowly, which means we will have a list of `n` copied of pointers, who are equal to each other and pointing to the same data in memory.
Look at an example in python repl:
```python
>>> arr2d_wrong = [[None] * 3] * 2 # 2x3 2-d array
>>> arr2d_wrong
[[None, None, None], [None, None, None]]
>>> arr2d_wrong[0][0] = 7 # change first element of first array
>>> arr2d_wrong
[[7, None, None], [7, None, None]] 
```

Here the code looks like it only wants to change the first element of the first array. But, in reality, it changes the first element of all arrays.

The other method is fine:
```python
>>> arr2d = [[None for _ in range(3)] for _ in range(2)]
>>> arr2d
[[None, None, None], [None, None, None]]
>>> arr2d[0][0] = 7
>>> arr2d
[[7, None, None], [None, None, None]]
```

If we inspect the memory address, it's going to be exactly what I explained before. In python, instead of memory address, checking the object id does the same thing.
```python
>>> [id(l) for l in arr2d_wrong]
[140260152665728, 140260152665728]
>>> [id(l) for l in arr2d]
[140260150944704, 140260153395264]
```

The correct technique has a list of *independent* lists while the wrong method does not.

## Why it worked?

Why the "wrong" technique worked in 1-d arrays?
Because `None` is a singleton in Python. And it's immutable. When we assign a new value to the element in the list, we are changing the data by also changing the reference, instead of just mutate the value of an object.
- 