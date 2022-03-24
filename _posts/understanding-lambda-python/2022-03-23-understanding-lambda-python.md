---
layout: post
author: "0x4f5041"
title: Lambda functions in Python
icon: python
date: 2022-03-23 16:54 -03:00
modified: 
tags: [python]
description:  Understanding lambda functions in Python
---

<figure>
<img src="/understanding-lambda-python/lambda-banner.png" alt="working with ambda functions in Python">
</figure>


### Lambda introduction
The lambda functions or also called _anonymous functions_, is the same as a normal function but without a defined name.
It's usually used when it is required to use a function for a short period of time.

The main properties of lambda functions are:

- it's an anonymous function, has no name.
- it can receive any number of arguments
- The lambda body has a **return**

### Coding example
The structure of a function that returns a number + 1 is:
```python
>>> def add(x):
...     return x+1
...
>>> add(2)
3
>>> add(3)
4
>>> add(6)
7
```

You can get the same result using *lambda*, coding it in one line.

```python
>>> add_one = lambda x : x + 1
>>>
>>> add_one(2) # lambda 2 : 2 + 1 = 3
3
>>> add_one(3) # lambda 3 : 3 + 1 = 4
4
```

It's possible to pass an argument using parentheses
```python
>>> (lambda x: x**2)(5)
25
>>> (lambda x, y: x + y)(7,10)
17
```

### Another coding example

Lets use a lambda function to apply the [OR](https://en.wikipedia.org/wiki/Logical_disjunction) logic.

```python
>>> logic_or = lambda x, y: x or y
>>> for i in range(2):
...     for j in range(2):
...         print(f'{i} or {j} = {logic_or(i, j)}')
...

0 or 0 = 0
0 or 1 = 1
1 or 0 = 1
1 or 1 = 1
```
