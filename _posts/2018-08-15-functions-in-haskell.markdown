---
layout: post
title:  "Functions in Haskell"
date:   2018-08-15 16:45:00 +0530
categories: jekyll update
---

Calling up a function is as simple as specifying the function name, followed by the parameters. Parenthesis is optional, just like in Ruby.

```
max 12 (-12)
```
```
λ: max 12 (-12)
12
```

Defining a function is similar to calling it.

```
doubleMe x = x + x
```
```
λ: doubleMe 21
42
```

Function with an `if...else`.
```
odd' x = if x `mod` 2 == 0 then True else False
```

**Note:** In Haskell, there has to be a mandatory `else` block for every `if`. That's basically because `if` statement is an expression and must evaluate to some value.

**Note 2:** There is no `else if` statement in Haskell. We use pattern matching or guards for such use cases.

We can call and assign values from function return:
```
λ: is_odd = odd' 27
λ: is_odd
True
λ:
```

If you notice `is_odd` also defined exactly like a function is like. A function without parameters is called a `definition` in Haskell.

# References

* [Starting out Haskell - Learn You Haskell][starting-out-haskell]

[starting-out-haskell]: http://learnyouahaskell.com/starting-out