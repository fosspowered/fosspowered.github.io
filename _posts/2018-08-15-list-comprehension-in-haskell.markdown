---
layout: post
title:  "List Comprehension in Haskell"
date:   2018-08-15 17:55:00 +0530
categories: programming haskell
---
* TOC
{:toc}

## Basic Usage

```
[x ^ 2 | x <- [1..25], x `mod` 2 == 1]
```

This will get all squares of odd numbers between 1 and 25.

```
λ: [x ^ 2 | x <- [1..25], x `mod` 2 == 1]
[1,9,25,49,81,121,169,225,289,361,441,529,625]
```

This is very similar to a set comprehesion.

The filtering is not mandatory.

```
[x ^ 2 | x <- [1..10]]
```
```
λ: [x ^ 2 | x <- [1..10]]
[1,4,9,16,25,36,49,64,81,100]
```

### Multiple predicates

We can have several predicates.

```
[ x | x <- [10..20], x /= 13, x /= 15, x /= 19]
```


### Draw from multiple lists

This will basically get all combinations from multiple lists.

```
[ (x, y, z) | x <- [1..2], y <- [3..4], z <- [5..6] ]
```

We can even add a filter.

```
λ: [ (x, y, z) | x <- [1..2], y <- [3..4], z <- [5..6], x < y, y < z]
[(1,3,5),(1,3,6),(1,4,5),(1,4,6),(2,3,5),(2,3,6),(2,4,5),(2,4,6)]
```

## Examples

### Fizz, no buzz

For example if we want to write a program which takes a list and returns "Fizz!" if the number is divisible by 3 but if not then the number itself.

{% highlight haskell %}
fizz xs = [if x `mod` 3 == 0 then "Fizz" else show x | x <- xs]
{% endhighlight %}

```
λ: fizz xs = [if x `mod` 3 == 0 then "Fizz" else show x | x <- xs]
λ: fizz [1..10]
["1","2","Fizz","4","5","Fizz","7","8","Fizz","10"]
λ: fizz []
[]
```

### Length of a list

{% highlight haskell %}
length' xs = sum [1 | x <- xs]
{% endhighlight %}

```
λ: length' "abc"
3
λ: length' [1..100]
100
```

### Remove uppercase chars

{% highlight haskell %}
removeUppercase xs = [x | x <- xs, x `notElem` ['A'..'Z']]
{% endhighlight %}

```
λ: removeUppercase xs = [x | x <- xs, x `notElem` ['A'..'Z']]
λ: removeUppercase "thiISs iSs aA sTRINGtr"
"this is a str"
```

# References

* [Starting out Haskell - Learn You Haskell][starting-out-haskell]

[starting-out-haskell]: http://learnyouahaskell.com/starting-out