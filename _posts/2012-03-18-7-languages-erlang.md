---
layout: post
title: "7 Languages: Erlang"
category: technical
tags:
    - erlang
    - programming languages
    - 7 Languages in 7 Weeks
---
Chapter 5 of 7 Languages in 7 Weeks is on [Erlang](http://en.wikipedia.org/wiki/Erlang_(programming_language)).  Erlang is a functional language with a strong focus on concurrency and reliability.  Its syntax is based on Prolog (i.e. it's weird).  The author described it as a language that "makes easy things hard, and hard things easy".

As a functional language it has a lot of functions geared towards collection operations (e.g. map, foreach, foldl).  Nothing terrible weird about those.  It does have this cool feature they call list comprehensions, that are a way for you to combine most of those operations into one line:

```erlang
//rough syntax
[map || iteration, filter, filter2, ...]

//example
[lists:foldl(fun(X, Product) -> X * Product end, List) || List <- Lists, length(List) > 5]
```

This will return a list that contains the product of all elements in each list with a length longer than 5.

But in general the syntax and general usage is the "making easy things hard" part of that quote.  The "making hard things easy" part is related to concurrency and reliability.

Erlang also uses an actor based concurrency strategy, but rather than having them run in threads as they would in Scala, Erlang spawns lightweight processes.  Those processes don't share any state, pushing developers even farther down the immutability only and functional programming route.

The reliability portion of that is that there are some core libraries that help manage the processes and restart them if they fail.  Rather than burden the code with all kinds of error handling logic, Erlang's mantra is "let it crash".  If the process fails you have something monitoring for that and it is immediately restarted.

Erlang seems well suited to a lot of things.  Most of them aren't things I'm interested in developing.  I'm glad to have learned a little about their perspective, but I'm not too broken up about moving on to the next language: Clojure.
