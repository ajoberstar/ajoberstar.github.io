---
layout: post
title: Relearning PHP
category: technical
tags:
    - php
    - programming languages
---
Very little of my programming life has been outside of the JVM world.  Java was the primary language at my college, and is the primary language at my workplace.  Recently, I've gotten into Groovy, which is a dynamic language for the JVM.  I dabbled a small amount in C++ and PHP, but didn't stick with them.

I recently began collaborating with a friend on a website, so I've been trying to relearn PHP which is our common denominator.  I read through most of the manual on php.net, but needed something that gave a little more

In general, I have a bad view of PHP as an Object Oriented language.  This mainly stems from its beginnings as a simple scripting language and having objects tacked on once people started using it for more complex use cases.  PHP's OO capabilities just doesn't seem mature to me.  I've only been developing in PHP for about a week (with not a whole lot of code generated), but I loath it.  I'm sure a large factor is my background in Java, which makes many aspects of PHP sit funny with me.

- Dynamic typing:
    - Groovy has dynamic types too but, in practice, I usually specify my types.  It is a rare case for me where I want the flexibility of a dynamic type at the cost of the clarity a specified type provides.  You can't really program to an interface when you could theoretically return anything from any method.
    - Not being able to specify the return types of methods makes it very hard for me to understand what's going on at a glance.
- Automatic conversions based on context:
    - Again something that Groovy does, but I have a better grasp of the semantics with Groovy.  Chalk that up to lack of experience with PHP.
- Lacking per-application module use (at least from my understanding):
    - In JVM languages you add a JAR to your classpath in order to use a module/library.  This gives you a lot of flexibility in per-application dependency management and portability.
    - PHP seems to require that you install modules in a per-installation extensions directory.  At least for me, this causes a lot of config issues when moving between servers.
- Clumsy file/module/class inclusion:
    - Yet another Java bias...  I like the fact that Java gives me automatic access to any class that is present on the classpath.  I don't want to use a require directive to specify the specific file I should load from.
    - I could write an autoloading block, but why should I have to do that when I feel the interpreter could handle that for me if given a classpath-like input.

I do still want to expand my language horizons, though I don't plan on PHP being anything more than a short-term part of that.  I'm considering picking up [7 Languages in 7 Weeks](http://www.amazon.com/Seven-Languages-Weeks-Programming-Programmers/dp/193435659X) in the next few months.  The goal of this book is to give you an intro-level flavor of seven languages: Ruby, Io, Prolog, Scala, Erlang, Clojure, Haskell.  That seems like it would be a good starting point on finding a new language to make a deeper dive into.
