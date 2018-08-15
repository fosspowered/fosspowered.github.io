---
layout: post
title:  "Starting Haskell"
date:   2018-08-15 16:30:00 +0530
categories: haskell programming
---
We use `GHCi` for interactive programming with Haskell.

{% highlight bash %}
Configuring GHCi with the following packages:
GHCi, version 8.4.3: http://www.haskell.org/ghc/  :? for help
Prelude>
{% endhighlight %}

Simple arithmetic:
{% highlight haskell %}

Prelude> 10 + 9
19
Prelude> 12 - 4
8
Prelude> 18 * 3
54
Prelude> 12 / 2
6.0
Prelude> 13 `mod` 2
1
Prelude> 2 ^ 5
32
Prelude> (3 + 5) ^ 2
64
{% endhighlight %}

**Note:** Unlike typical languages, Haskell requires unary operator (-) to be used with parenthesis, when used after an operator. The compiler complains otherwise.

{% highlight haskell %}
Prelude> -2 * 3
-6
Prelude> 2 * -3

<interactive>:16:1: error:
    Precedence parsing error
        cannot mix ‘*’ [infixl 7] and prefix `-' [infixl 6] in the same infix expression
Prelude>
{% endhighlight %}

The inequality operator is not `!=`, it is `/-`.

`succ` finds the successor and `pred` finds the predecessor.

`max` finds the maximum within 2 inputs while `min` finds minimum.

When a function takes two parameters (two operands), its usage can be used like the regular function call:

```
max 3 2
```

However it can also be used as an infix operator.

```
3 `max` 2
```

# References

* [Starting out Haskell - Learn You Haskell][starting-out-haskell]

[starting-out-haskell]: http://learnyouahaskell.com/starting-out
