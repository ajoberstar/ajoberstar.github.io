---
layout: post
title: "7 Languages: Io"
date: 2012-03-10 00:00:00
category: technical
tags:
    - io
    - programming languages
    - 7 Languages in 7 Weeks
---
Chapter 2 of 7 Languages in 7 Weeks is on the [Io programming language](http://en.wikipedia.org/wiki/Io_(programming_language)).  Io is a prototypical (like JavaScript) object oriented language.  JavaScript usually gives me a bad taste in my mouth, because the prototype style just doesn't feel right.  However, now that I have more experience with Io's prototyping, I can see the power.  I wouldn't want to build an application with prototypes, but I see now that they have their place.

You create new objects by cloning other ones:

```io
myObject  := Object clone
```

You can add properties (not the Io term for it) and methods to slots on the object:

```io
myObject name := "Test"

myObject printName := method(name println)
```

Surprisingly the prototype system wasn't the interesting part of Io (at least for me).  Io's syntax is as simple as it gets.  All actions happen through message passing.  For example a Hello World program looks like this:

```io
"Hello World" println
```

Seems backwards at first, but what's happening is that "Hello World" is the object and println is the message being sent to it. Pretty much the only two other pieces of syntax are arguments on method calls (no argument methods can be called with parens):

```io
myObject doStuff(arg1, arg2)
```

and operators (which are really just specially parsed messages:

```io
myObject := Object clone
```

that parses to:

```io
myObject :=(Object clone)
```

That's it.  There are no keywords, there's no syntactic sugar, none of the stuff I usually expect to have to learn with a new language. What you end up with is just learning the libraries that are provided, which is a chore and a half.  I haven't been able to find a good reference of the available methods.  I ended having to resort to using the "slotNames" slot of the major prototypes to get any idea of what was available.  All you get there is the names, so there's not always a clear indication of what it does or what kind of arguments it expects.

Dealing with the normal libraries would have been enough challenge, but the 3rd set of exercises focused on metaprogramming.  You have a lot of power to change the way that Io works.  You can create new operators, change the behavior of any method on any object.  A couple of the examples were for creating new map and list syntaxes which was pretty cool.

Inside of a method you can get all kinds of information about the message that is being invoked.  Unfortunately there isn't much documentation on how to access or use that information.

I learned far more from Io than I did from Ruby, but  I don't see Io as a language I would write applications in.  It has a lot to teach, especially if you come from a Java background.  There's also some intriguing concurrency support, that the book gave only a passing discussion of.

Next up, Prolog!
