---
layout: post
title:  "List Ranges in Haskell"
date:   2018-08-15 17:30:00 +0530
categories: haskell programming
---
* TOC
{:toc}

# Defining ranges

Range can be defined in Haskell by using the `..` operator within a list definition.
```
[1..9]
```
```
λ: [1..9]
[1,2,3,4,5,6,7,8,9]
```

**Note**: The range in Haskell is inclusive of both the first and last elements, unlike in Python where it it does not include the right term.

We can also use floating point terms but they are not recommended due to precision problems with floating point numbers.

We can use infinite lists in combination of `take` to get the numbers we require.

```
λ: take 10 [9,18..]
[9,18,27,36,45,54,63,72,81,90]
λ:
```

# Steps

We can also specify stepping in Haskell lists by specifying the first two elements and the last element.

```
[1,3..9]
[9,8..(-1)]
```
```
λ: [1,3..9]
[1,3,5,7,9]
λ: [9,8..(-1)]
[9,8,7,6,5,4,3,2,1,0,-1]
```

# Functions producing infinite lists

`cycle` takes a list and cycles it into an infinite list. If used directly it will create an infinite loop. It has to be sliced.
```
λ: take 10 (cycle [1..3])
[1,2,3,1,2,3,1,2,3,1]
```

`repeat` takes an element and produces an infinite list of just that element. It's like cycling a list with only one element.
```
λ: take 5 (repeat 10)
[10,10,10,10,10]
```

`replicate` is more useful in this context.
```
λ: replicate 10 3
[3,3,3,3,3,3,3,3,3,3]
```

# References

* [Starting out Haskell - Learn You Haskell][starting-out-haskell]

[starting-out-haskell]: http://learnyouahaskell.com/starting-out