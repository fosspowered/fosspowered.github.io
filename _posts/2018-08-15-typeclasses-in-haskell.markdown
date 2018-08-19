---
layout: post
title:  "Typeclasses in Haskell"
date:   2018-08-15 20:00:00 +0530
categories: programming haskell
---
* TOC
{:toc}

A typeclass is a sort of interface which defines a behaviour. They are kind of like interfaces in Java in the sense if a type is a part of a typeclass it must implement the behaviour the typeclass specifies.

For example, what is type signature of `==`:

```
λ: :t (==)
(==) :: Eq a => a -> a -> Bool
```

The part between `::` and `=>` is the class constraint. Here it specifies that there is only one type supported for this operation parameters (`a`) and that type must be part of the typeclass `Eq`.

Similarly:

```
λ: :t (>=)
(>=) :: Ord a => a -> a -> Bool
```

Here, it is specifying that the input params must be of same type and they must implement the typeclass `Ord`.

The `elem` function has the type:

```
λ: :t elem
elem :: (Foldable t, Eq a) => a -> t a -> Bool
```

Here the type of the element and the element array individual element must be same and that type should implement `Eq`.

For example this won't work: `elem 'dog' [1, 2, 3]`.

## Basic Typeclasses

### Eq
`Eq` used for types that support equality testing. They implement: `==` and `/=`.	

```
λ: 5 == 5
True
λ: 4 == 5
False
λ: 4 /= 5
True
λ: 4 /= 4
False
```

### Ord
`Ord` used for types that support ordering. They implement `>`, `>=`, `<`, and `<=`.

The `compare` function takes two `Ord` values and returns an enum: `EQ`, `LT`, `GT`.

```
λ: :t compare
compare :: Ord a => a -> a -> Ordering
λ: compare 2 2
EQ
λ: compare 2 1
GT
λ: compare 2 3
LT
λ: LT
LT
```

### Show and Read
`Show` members can be presented as strings. It's equivalent to the method `toString` in Java and `__str__` in python. They implement the `show` method.

```
λ: show 3
"3"
λ: show "Cat"
"\"Cat\""
λ: show 'c'
"'c'"
λ: show True
"True"
```

`Read` is sort of the opposite typeclass of Show. The read function takes a string and returns a type which is a member of Read. They implement the `read` method.

```
λ: read "8" :: Int
8
λ: read "8.2" :: Float
8.2
λ: read "True" :: Bool
True
```

Please note `read` method needs an inference type to figure out the type of the result. Without that it won't be able to figure out to which type's read method would be call. That is done by `::`.

### Enum

`Enum` members are sequentially ordered types with names. We can use them in ranges (as they are ordered). They implement the `succ` and `pred` methods.

```
λ: ['a'..'e']
"abcde"
λ: [LT .. GT]
[LT,EQ,GT]
λ: [3 .. 5]
[3,4,5]
λ: succ 'q'
'r'
λ: pred 43
42
```

### Bounded

`Bounded` members have a upper and a lower bound. They implement the `minBound` and `maxBound` methods.

```
λ: minBound :: Int
-9223372036854775808
λ: minBound :: Char
'\NUL'
λ: minBound :: Bool
False
λ: maxBound :: Bool
True
λ: maxBound :: Char
'\1114111'
λ: maxBound :: Int
9223372036854775807
```

### Num

`Num` is a numeric typeclass. Its members basically have to behave like well...a number.

Numeric literals practically act like polymorphic constants. They can act like any type that's a member of the `Num` typeclass.

```
λ: 20 :: Int
20
λ: 20 :: Integer
20
λ: 20 :: Float
20.0
λ: 20 :: Double
20.0
```

To join `Num` the type must satisfy both `Show`, and `Eq` as well as a glut of other operations.

Examining the `Num` operators `+`, `-`, `*`.
```
λ: :t (+)
(+) :: Num a => a -> a -> a
λ: :t (-)
(-) :: Num a => a -> a -> a
λ: :t (*)
(*) :: Num a => a -> a -> a
```

* `Integral` is also a numeric typeclass. `Num` includes all numbers, including reals and integral numbers, Integral includes only integral (whole) numbers. In this typeclass are Int and Integer.
* `Floating` includes only floating point numbers, so Float and Double.
* `Fractional` is any kind of number for which we can define a division. It's a superset of `Floating`.

`/`, `mod` are fractional, integral respectively and `^` only supports an integral power.
```
λ: :t (/)
(/) :: Fractional a => a -> a -> a
λ: :t (mod)
(mod) :: Integral a => a -> a -> a
λ: :t (^)
(^) :: (Integral b, Num a) => a -> b -> a
```

A very useful function for dealing with numbers is `fromIntegral`.

```
fromIntegral :: (Integral a, Num b) => a -> b
```

It takes an integral number and converts it into a more generic number to perform operations such that it works nicely with floating point numbers.


## References

* [Types and Typeclasses][haskell-tut]

[haskell-tut]: http://learnyouahaskell.com/types-and-typeclasses