---
layout: post
title:  "Tuples in Haskell"
date:   2018-08-15 18:30:00 +0530
categories: programming haskell
---
* TOC
{:toc}

Similar to lists, tuples are a way to store multiple values into a single unit. However unlike a list, tuple elements can be of different types. So a tuple like `("dog", 23, 'l', 3.0)` is valid.

However tuple itself has a type:

```
λ: :t (1, 2, 3)
(1, 2, 3) :: (Num a, Num b, Num c) => (a, b, c)
λ: :t ("dog", 23, 'l', 3.0)
("dog", 23, 'l', 3.0)
  :: (Fractional d, Num b) => ([Char], b, Char, d)
```

You could create a list with elements: `[[1,2],[1,2,3],[2,3]]`, since each element is a list of numbers so are of same type. However you cannot create a list likeL `[(1,2), (1,2,3), (2,3)]` because `(2,3)` is a different type than `(1,2,3)`.

```
λ: :t [1, 2]
[1, 2] :: Num a => [a]
λ: :t [1, 2, 3]
[1, 2, 3] :: Num a => [a]
λ: :t (1, 2)
(1, 2) :: (Num a, Num b) => (a, b)
λ: :t (1, 2, 3)
(1, 2, 3) :: (Num a, Num b, Num c) => (a, b, c)
```

Tuples are much more rigid because each different size of tuple is its own type, so you can't write a general function like `sum`, `elem` for a tuple. You have to write functions for every type of tuple: 2-element, 3 element.

## Operations on Tuples

`fst` takes a pair and returns its first component.
```
fst ("cat", "dog")
```
```
λ: fst ("cat", "dog")
"cat"
```


`snd` takes a pair and returns its second component.
```
snd ("cat", "dog")
```
```
λ: snd ("cat", "dog")
"dog"
```

`zip` in haskell is similar to its counterpart in Python. If one list is longer than the other, the longer list elements are ignored. It's lazy like everything else in Haskell and hence can be used to zip infinite lists with finite ones.
```
zip [1,3..10] [2,4..10]
```
```
λ: zip [1,3..10] [2,4..10]
[(1,2),(3,4),(5,6),(7,8),(9,10)]
λ: zip [1,3..10] [100..]
[(1,100),(3,101),(5,102),(7,103),(9,104)]
```

Get all right triangles which have lengths less than 10 and perimeter is 24.

{% highlight haskell %}
[(a, b, c) | c <- [1..10], b <- [1..9], a <- [1..b], a ^ 2 + b ^ 2 == c ^ 2, a + b + c == 24]
{% endhighlight %}
```
λ: [(a, b, c) | c <- [1..10], b <- [1..9], a <- [1..b], a ^ 2 + b ^ 2 == c ^ 2, a + b + c == 24]
[(6,8,10)]
```

# References

* [Starting out Haskell - Learn You Haskell][starting-out-haskell]

[starting-out-haskell]: http://learnyouahaskell.com/starting-out