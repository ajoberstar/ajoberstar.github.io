---
layout: post
title: "7 Languages: Ruby"
guid: 5005ed49e4b0d534734f5630:5005f070e4b0ee36c463b555:5005f070e4b0ee36c463b585
category: technical
tags:
    - ruby
    - programming languages
    - 7 Languages in 7 Weeks
---
I did end up buying [Seven Languages in Seven Weeks](http://pragprog.com/book/btlang/seven-languages-in-seven-weeks).  This book covers the following languages:

- [Ruby](http://en.wikipedia.org/wiki/Ruby_(programming_language))
- [Io](http://en.wikipedia.org/wiki/Io_(programming_language))
- [Prolog](http://en.wikipedia.org/wiki/Prolog)
- [Scala](http://en.wikipedia.org/wiki/Scala_(programming_language))
- [Erlang](http://en.wikipedia.org/wiki/Erlang_(programming_language))
- [Clojure](http://en.wikipedia.org/wiki/Clojure)
- [Haskell](http://en.wikipedia.org/wiki/Haskell_(programming_language))

This book isn't trying to teach the details of all 7 languages.  The author admits that would be a foolish pursuit.  Instead, each chapter is designed to give you a flavor for what makes the language unique.  What I found most interesting is that the author (Bruce Tate) doesn't actually teach you how to do most of the exercises.  He gives some examples that give you a taste, but trusts that you are smart enough to use Google to find some reference material.

I just finished the Ruby section, so here's my take on the language.  I won't bother describing what Ruby is for two reasons:  it's insanely popular right now (Ruby on Rails) and that's what [Wikipedia's](http://en.wikipedia.org/wiki/Ruby_(programming_language)) for.

The biggest thing that struck me as I learned some of the features of Ruby, was how similar it is to Groovy.  Groovy is an extension of Java that provides a lot (I mean a lot) of the features Ruby does.  Groovy isn't as pure as Ruby, given it's deep tie into Java, but it helped me pick up a lot of the concepts very quickly.

Some key features:

- [duck typing](http://en.wikipedia.org/wiki/Duck_typing) - No need to check types.  As long as the (If it has a swim method like a Duck, has a quack method like a Duck, might as well treat it like a Duck)
- [metaprogramming](http://en.wikipedia.org/wiki/Metaprogramming) - Can change the way a class behaves (add new methods, override existing methods, etc) at runtime.  Groovy has this with the metaclass.
- blocks (i.e. closures) - Functions are objects.  They can be passed as arguments to other functions/methods.

Ruby as a language seems pretty interesting.  Tate talked about how Ruby is great for rapid development.  One of the reasons I've been wary about Ruby before is the performance.  However, Tate points out that worrying about performance before you even having anything is pointless pre-optimization.  Better to develop something quickly that might perform poorly, if you get a significant user base, than never finish something on pure Java because there's so much extra code to write.  Though since I can do most of the same stuff in Groovy, and I'm already familiar with it, I'm not sure how likely it is I'll use Ruby for anything.

JRuby (an implementation of Ruby for the JVM) is also interesting to me.  I've never used Ruby's gem system from a programming standpoint, but I have tried to install ruby apps before.  When I tried installing [Gitorius](http://gitorious.org/) there were so many ruby dependencies to deal with installing, that I never got it to work.  It just wasn't worth the time.  I'm hoping that JRuby has a nicer way of managing its gem equivalents.
