---
layout: post
title: "7 Languages: Haskell"
category: technical
tags:
    - haskell
    - programming languages
    - 7 Languages in 7 Weeks
---
The final language of 7 Languages in 7 Weeks was [Haskell](http://en.wikipedia.org/wiki/Haskell_(programming_language)), the only pure functional language in the book.  This is the only chapter where I completely gave up on most of the exercises.  More on that later...

Haskell as a functional language does a lot of the things I've seen in half the languages in the book.  It has a list comprehension syntax almost identical to Erlang's, the common list manipulation functions like map, filter, and foldl, as well as pattern matching.  Here's one example of a Haskell function:

```haskell
allEven [] = []
allEven (h:t) = if even h then h:allEven t else allEven t
```

One of the biggest differences with Haskell compared to the other functional languages in the book is its strong, static type system.  Like Scala, a lot of the types are inferred from the context.  The author really hyped it up, so I thought it would be pretty intuitive.  Once I dug into the second set of exercises, however, I was baffled.  I tried making a function for removing an item from a list:

```haskell
listRemove :: [Integer] -> Integer -> [Integer]
listRemove list x = foldl (\elem result -> if x == elem then result else elem:result) [] list
```

Seemed like it should work to me.  However when I compiled it, I got this:

```
Couldn't match expected type `[Integer]' with actual type `Integer'
In the first argument of `listRemove', namely `min'
In the first argument of `sort', namely `(listRemove min list)'
In the second argument of `(:)', namely
  `(sort (listRemove min list))'
Failed, modules loaded: none.
```
While, at first glance, that appears to be a well described error, I can't for the life of me figure out why elem is being treated as a [Integer] rather than a Integer...  And that right there is where I stopped doing the exercises.

Onle last feature of Haskell that I'll mention is that you can only declare functions with one argument.  You can essentially create multi-argument functions, but they're actually "curried" to form the end result.

```haskell
-- function with two parameters (kind of)
product x y = x * y

-- calling product 3 4 is equivalent to
(product 3) 4
```

This happens because the function "product" doesn't take two arguments.  The type declaration for this would be:

```haskell
double :: Integer -> Integer -> Integer
```

Which means product is a function that takes one Integer but returns a function that takes one more Integer which then returns an Integer.  Pretty interesting concept.

There was another chapter on declaring types and monads which went almost completely over my head.  It didn't help that I was alteady frustrated with Haskell and didn't really care how it worked anymore.

Haskell seems like it would teach me a lot about functional programming, but I don't have any intention of looking at it anytime soon.  I'm sure it would be a lot easier to understand with a book tailored towards teaching the language rather than just getting a taste of what it has to offer.

I've got one more post coming to wrap up the 7 Languages book.
