---
layout: post
title:  "Lists in Haskell"
date:   2018-08-15 16:55:00 +0530
categories: programming haskell
---
* TOC
{:toc}

# Defining lists
In Haskell, lists are defined in a similar way as they're defined in Python. However a list in Haskell in homogenous. So we _cannot_ have a list like: `[23, "Dog", 'c']`.

```
l = [1, 2, 3]
```

Lists can also contain lists. They can also contain lists that contain lists that contain lists.
```
λ: [[1,2],[3,4],[5,6],[7,9],[9]]
[[1,2],[3,4],[5,6],[7,9],[9]]
λ: [[[1,2],[3,4]],[[5,6],[7,8]]]
[[[1,2],[3,4]],[[5,6],[7,8]]]
```


# Operations on lists

Joining two lists is done using the `++` operator.
```
l = [1,2,3] ++ [4,5,6,7,8,9]
```
```
λ: l = [1,2,3] ++ [4,5,6,7,8,9]
λ: l
[1,2,3,4,5,6,7,8,9]
```

Internally, Haskell walks through the left list operand, hence this operation would be expensive for a long left hand list.

We can use this syntax to append an element as well:
```
λ: [0] ++ [1,2,3]
[0,1,2,3]
```

However we can use the `:` operator which is a syntactic sugar for the above operator.
```
0 : [1, 2, 3]
```
```
λ: 0 : [1, 2, 3]
[0,1,2,3]
```

We can use the equality operators: `==`, and `/=` in Haskell.

We can use `>`, `<`, `>=`, `<=` relational operators as well. Comparison is by lexicographical order element-wise.


# Basic Functions

`head` takes a list and gives the first element.

```
head [3, 7, 4]
```
```
λ: head [3, 7, 4]
3
```

`tail` takes a list and returns all elements except the last element.
```
tail [3, 7, 4]
```
```
λ: tail [3, 7, 4]
[7, 4]
```

`last` takes a list and gives the last element.
```
last [3, 7, 4]
```
```
λ: last [3, 7, 4]
4
```

`init` takes a list and gives all elements except the last one.
```
init [3, 7, 4]
```
```
λ: init [3, 7, 4]
[3, 7]
```

`null` checks if a list is empty. If it is, it returns True, otherwise it returns False.
```
null []
```
```
λ: null [3, 7, 4]
False
λ: null []
True
```

`reverse` reverses a list.
```
reverse [3, 2, 1]
```
```
λ: reverse [3, 2, 1]
[1,2,3]
```

`take` takes number and a list. It extracts that many elements from the beginning of the list.
```
take 4 [2, 4, 6, 8, 1, 3, 5, 7]
```
```
λ: take 4 [2, 4, 6, 8, 1, 3, 5, 7]
[2,4,6,8]
```

`drop` works in the opposite manner. It drops that many elements from the end and returns the rest of the list.
```
drop 2 [2, 4, 6, 8, 1, 3, 5, 7]
```
```
λ: drop 2 [2, 4, 6, 8, 1, 3, 5, 7]
[6,8,1,3,5,7]
```

**Note:** These operations cannot be performed on an empty list. An error is thrown in that case.


`maximum` gives the maximum value in the list if the element type defines same kind of order. Similar for `minimum`. Please note this is _different_ from `max` and `min` functions which work with 2 elements.
```
maximum [3, 0, 2, 9, 1]
minimum [3, 0, 2, 9, 1]
```
```
λ: maximum [3, 0, 2, 9, 1]
9
λ: minimum [3, 0, 2, 9, 1]
0
λ:
```

`sum` and `product` take the sum and product of the elements in the list.
```
sum [1, 2, 3, 4]
product [1, 2, 3, 4]
```
```
λ: sum [1, 2, 3, 4]
10
λ: product [1, 2, 3, 4]
24
λ:
```

Elem takes an element and a list and returns whether the element is member of the list.
```
elem 4 [1, 4, 9]
4 `elem` [1, 4, 9]
0 `elem` [2, 3]
```
```
λ: elem 4 [1, 4, 9]
True
λ: 4 `elem` [1, 4, 9]
True
λ: 0 `elem` [2, 3]
False
λ:
```

Similarly we have `nonElem` which does the opposite.


# References

* [Starting out Haskell - Learn You Haskell][starting-out-haskell]

[starting-out-haskell]: http://learnyouahaskell.com/starting-out