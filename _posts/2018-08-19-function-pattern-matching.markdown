---
layout: post
title:  "Pattern Matching in functions"
date:   2018-08-18 20:00:00 +0530
categories: programming haskell
---
* TOC
{:toc}

## Basic Pattern Matching

When defining functions in Haskell, we can define separate function bodies for different patterns.

```
luckySeven :: (Integral a) => a -> String
luckySeven 7 = "Today's your lucky day."
luckySeven x = "Not your lucky day."
```

When we call a function like this, we check the patterns from top to bottom and once we find the match we use that particular function body.

Factorial with pattern matching:
```
factorial' :: (Integral a) => a -> a
factorial' 0 = 1
factorial' n = n * factorial' (n - 1)
```

This is a common paradigm used in Haskell for recursion. Specifically define for edge cases and then write your base case.

Pattern matching can fail if we do not match any function body for the given input. For example:

```
λ> say 1 = "One"
λ> sayOne 1
1
λ> sayOne 2
*** Exception: <interactive>:46:1-12: Non-exhaustive patterns in function sayOne
```

## Pattern matching with tuples

Pattern matching can also be used in tuples. For example vector addition:

```
addVectors :: (Num a) => (a, a) -> (a, a) -> (a, a)
accVectors (x1, y1) (x2, y2) = (x1 + x2, y1 + y 2)
```

`fst` and `snd` get first and second elements of tuple pairs. What if we want for triplets.
```
fst' :: (a, b, c) -> a
fst' (x, _, _) = x

snd' :: (a, b, c) -> a
snd' (_, y, _) = y

thr' :: (a, b, c) -> a
thr' (_, _, z) = z
```

The `_` means that the value exists but has no meaning for our function so we don't use it.

As a side note, we can also pattern match in list comprehenshion.

```
λ: let pairs = [("Horse", "Mare"), ("Lion", "Lioness"), ("Fox", "Vixen")]
λ: [a ++ " and " ++ b | (a, b) <- pairs]
["Horse and Mare","Lion and Lioness","Fox and Vixen"]
```


## Pattern Matching with lists

Lists can also be used for pattern matching. They can match with empty list, or any pattern that involves `:` and an empty list. Effectively, `[1,2,3]` is just `1:2:3:[]`.

```
sayWhenOneTwoThree :: (Num a, Eq a) => [a] -> String
sayWhenOneTwoThree [1, 2, 3] = "One! Two! Three!"
sayWhenOneTwoThree _ = "Nothing to say"
```
```
λ: sayWhenOneTwoThree [1,2,3]
"One! Two! Three!"
λ: sayWhenOneTwoThree []
"Nothing to say"
```

Implementation of `head` function:
```
head' :: [a] -> a
head' [] = error "No head can be found for empty list"
head' (x:xs) = x
```
```
λ: head' [9, 12, 2]
9
λ: head' [12, 2]
12
```

The `x:xs` pattern is used a lot in context of recursive functions. The first part `x` will be the element and `xs` will be the rest of the list.

It can be used for first n elements:
```
sayElement :: (Show a) => [a] -> String
sayElement [] = "Empty list"
sayElement (x:[]) = "One element only that is: " ++ show x
sayElement (x:y:[]) = "Two elements, those are: " ++ show x ++ " and " ++ show y
sayElement (x:y:xs) = "More than two elements. First two are: " ++ show x ++ " and " ++ show y ++ " and rest: " ++ show xs
```

Re-implementation of `length`:
```
length' :: [a] -> Int
length' [] = 0
length' (x:xs) = 1 + length' xs
```

For `sum`:
```
sum' :: (Num a) => [a] -> a
sum' [] = 0
sum' (x:xs) = x + sum' xs
```

## Binding to names

We can also break something up according to a pattern and binding to names, while still keeping reference to the whole thing. We can do that by using `@` in front of the pattern.

```
firstLetter:: String -> String
firstLetter [] = "Empty string!"
firstLetter w@(x:xs) = "The first letter for " ++ w ++ " is " ++ [x] ++ " while the rest is: " ++ xs
```
```
λ: firstLetter "2001 : Year"
"The first letter for 2001 : Year is 2 while the rest is: 001 : Year"
```


## References

* [Syntax in functions][haskell-tut]

[haskell-tut]: http://learnyouahaskell.com/syntax-in-functions