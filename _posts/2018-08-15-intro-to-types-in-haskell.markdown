---
layout: post
title:  "Introduction to Types in Haskell"
date:   2018-08-15 20:00:00 +0530
categories: programming haskell
---
* TOC
{:toc}

Haskell has a static type system. The type of every expression is known at compile time. Also it has strict type checking which throws an error at compile time when invalid operations are being performed. Furthermore, Haskell has type inference as it can infer a type as we write it.

A type is a kind of label that every expression has. We can use `:t` in `GHCIi` to get the type.

Typical types:
```
λ: :t 'a'
'a' :: Char
λ: :t 1
1 :: Num p => p
λ: :t 0.1
0.1 :: Fractional p => p
λ: :t pi
pi :: Floating a => a
λ: :t "Hello world!"
"Hello world!" :: [Char]
λ: :t [1, 2, 3]
[1, 2, 3] :: Num a => [a]
λ: :t [1..10]
[1..10] :: (Num a, Enum a) => [a]
λ: :t (1, "cat")
(1, "cat") :: Num a => (a, [Char])
```

## Types in functions

Functions also have types. When writing functions, we can give them their own type declaration.

{% highlight haskell %}
removeUppercase :: [Char] -> [Char]
removeUppercase st = [ c | c <- st, c `notElem` ['A'..'Z']]
{% endhighlight %}

**Note**: Type declarations don't work in `GHCi`. So we can save the source in a module, load the module and execute.

```
λ: :l types
[1 of 1] Compiling Main             ( types.hs, interpreted )
Ok, one module loaded.
λ: removeUppercase "thiISs iSs aA sTRINGtr"
"this is a str"
λ: :t removeUppercase
removeUppercase :: String -> String
```

For `[Char] -> [Char]`, we can also define as `String -> String`. Indeed it shows that way in `GHCi`.

For multiple parameters, we specify the parameters with an arrow. There is no distiction for return value, except that it's the last item in the declaration.

{% highlight haskell %}
addThreeNumbers :: Int -> Int -> Int -> Int
addThreeNumbers n1 n2 n3 = n1 + n2 + n3
{% endhighlight %}

## Common types

* `Int`: It's 32 bit signed integer.
* `Integer`: It's basically used to represent large values. Similar to integers in Python.
* `Float`: Floating point numbers.
* `Double`: Double precision.
* `Bool`: Boolean type.
* `Char`: Character type.
* `[Char]`: String type. Note that it's really a list of characters.
## References

## Type Variables

Similar to generics in Java (sort of), type variables which are used to define polymorphic functions in Haskell.

For example:

```
λ: :t fst
fst :: (a, b) -> a
λ: :t snd
snd :: (a, b) -> b
```

Here we can see both functions take items of different (or same if a = b) types and return a value of first type in `fst` and second type in `snd`.

## References

* [Types and Typeclasses][haskell-tut]

[haskell-tut]: http://learnyouahaskell.com/types-and-typeclasses