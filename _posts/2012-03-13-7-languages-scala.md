---
layout: post
title: "7 Languages: Scala"
category: technical
tags:
    - scala
    - programming languages
    - 7 Languages in 7 Weeks
---
Just crossed the halfway point of 7 Languages in 7 Weeks with [Scala](http://en.wikipedia.org/wiki/Scala_(programming_language)).  This is a hybrid object-oriented and functional language.  It's a JVM based language, and provides interoperability with existing Java code.  Like, Java it has strong static typing.  Unlike Java, Scala can infer types in many cases, removing a lot of extra typing.  For example in Java:

```java
List<String> list = new ArrayList<String>();
```

And in Scala:

```scala
val list = List("string1", "string2")
```

Scala knows that since you created a list of two Strings, that you probably want that variable to be a List[String] variable.  That line is about two-thirsda as long as the equivalent in Java, not to mention that I already added two items to the list in Scala, as opposed to the empty Java list.

Scala also supports closures, has native support for XML, really cool pattern matching stuff, and some fancy concurrency stuff that I don't really grasp.

Native support for tuples which can give you essentially multiple return values:

```scala
def getName() {
  (first, last)
}
val (first, last) = getName()
println(first)
println(last)
```

It also has an equivalent of multiple inheritance or mixins, that they call Traits.  A trait is essentially an abstract class, but you can mix multiple traits into a single class.  (This is just an illustration of the idea, not sure if the syntax is completely right)

```scala
trait Greeter {
  def greet() = println("Hello!")
}

trait Helper {
  def help() = println("Can I help you?")
}

class Person(name: String) with Greeter, Helper
```

Scala seems very complex.  It's type system is really cool, but hard to wrap your head around.  Case in point, this example method signature:

```scala
def map[B, That](f: A => B)(implicit bf: CanBuildFrom[Repr, B, That]): That
```

I'd really like to get into Scala some more (just ordered [Programming in Scala](http://www.amazon.com/Programming-Scala-Comprehensive-Step---Step/dp/0981531644/ref=sr_1_1?s=books&ie=UTF8&qid=1331695083&sr=1-1), so I can do just that).  It seems like a nice next step past Java.  Giving some more modern constructs and simplifying some of the mundane ceremony in Java.

Next up Erlang...
