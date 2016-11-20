---
layout: post
title: Drinking the Clojure Kool-Aid
guid: 5005ed49e4b0d534734f5630:5005f070e4b0ee36c463b555:545c375ce4b06e0eec9c1701
category: technical
tags:
    - clojure
    - programming languages
---
As with [Scala](http://www.andrewoberstar.com/blog/2012/3/13/7-languages-scala.html), my first [experience with Clojure](http://www.andrewoberstar.com/blog/2012/3/18/7-languages-clojure.html) was the [7 Languages in 7 Weeks](https://pragprog.com/book/btlang/seven-languages-in-seven-weeks) book. That merely gave me a flavor of Clojure's syntax, but didn't lead me to the deep philosophical underpinnings behind Clojure. More recently, I've been watching a lot of Clojure talks and have found Rich Hickey (creator of [Clojure](http://clojure.org) to be a very inspiring speaker. His [Simple Made Easy](http://www.infoq.com/presentations/Simple-Made-Easy) talk is easily my favorite, where he lays out a clear distinction between the concepts of simple (as opposed to complex) and easy (as opposed to hard) and how certain programming constructs contain an inherent complexity. That talk also popularized the term **complect** (to intertwine or braid) within the Clojure community as a way of emphasizing the precise type of complexity that Clojure intends to avoid.

As I've read mailing list threads and blog posts and watched more talks by others in the Clojure community, it's clear that the philosophy behind Clojure has a profound resonance with them. It can sometimes seem like they all part of a cult led by Rich Hickey, however, I completely buy into it.

Here are some of the core tenets that I really appreciate, along with some of the corresponding Clojure features:

- Immutability should be the default. (persistent data structures)
- Mutability constructs should be safe. (refs, agents, atoms)
- Polymorphism can be done without inheritance. (protocols, multimethods)

While some of these are concepts that are often espoused by "good" programmers in many languages, Clojure goes to a great deal of effort to make these "simple" concepts "easy".
