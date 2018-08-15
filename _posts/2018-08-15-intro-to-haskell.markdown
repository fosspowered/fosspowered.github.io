---
layout: post
title:  "Introduction to Haskell"
date:   2018-08-15 16:00:00 +0530
categories: jekyll update
---
[Haskell][haskell-wikipedia] is a standardized, general-purpose compiled purely functional programming language, with non-strict semantics and strong static typing.

Haskell is a functional language, where we focus on functions which take immutable values as input and produce new values as output. Furthermore, Haskell is a lazy language and it defers computation until the result is actually needed.

Haskell has profoundly different paradigm of programming and hence a typical haskell program looks quite different than a traditional program in C, Python, or Java.

Sample program of quicksort in Haskell:

{% highlight haskell %}
quicksort :: Ord a => [a] -> [a]
quicksort []     = []
quicksort (p:xs) = (quicksort lesser) ++ [p] ++ (quicksort greater)
    where
        lesser  = filter (< p) xs
        greater = filter (>= p) xs
{% endhighlight %}

# References

* [Haskell introduction wiki][haskell-wiki]
* [Real World Haskell - Why Haskell?][real-world-haskell]

[haskell-wikipedia]: https://en.wikipedia.org/wiki/Haskell_(programming_language)
[haskell-wiki]: https://wiki.haskell.org/Introduction
[real-world-haskell]: http://book.realworldhaskell.org/read/why-functional-programming-why-haskell.html