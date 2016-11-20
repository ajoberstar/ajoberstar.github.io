---
layout: post
title: Adventures in Scala/Lift Part 1
guid: 5005ed49e4b0d534734f5630:5005f070e4b0ee36c463b555:5005f070e4b0ee36c463b595
category: technical
tags:
    - programming languages
    - scala
    - lift
---
After completing 7 Languages in 7 Weeks, I decided to start working on a project to get my feet wet in Scala.  For the past couple weeks I've been reading through [Programming in Scala](http://www.amazon.com/Programming-Scala-Comprehensive-Step-step/dp/0981531601), which is seemingly the definitive Scala book and is written by the language author.

I've really enjoyed a lot of Scala features so far:

- Type inference -  One of the advantages to dynamic languages is that you don't have to specify types.  Usually it's so obvious what type the value should be that it's just a waste of keystrokes to specify the type yourself.  Scala gives you the same benefit but with static types, so everything is still enforced by the compiler.

  In Java:
  ```java
  Map map = new HashMap(); //verbose...
  ```

  In Groovy:
  ```groovy
  def map = [:] //concise, but no type safety
  ```
  In Scala:

  ```scala
  var map = Map[String, String]() //concise, with type safety
  ```
- Traits - Traits are insanely flexible compared to being stuck with abstract classes and interfaces in Java.  Being able to mix in an arbitrary number of traits to add new behavior is so much nicer than being forced into a hierarchical structure all of the time.  One example I have found useful is a simple Logging trait to provide an instance value named "logger".
  ```scala
  trait Logging {
    private val logger = LoggerFactory.getLogger(getClass)
  }

  class LogActor extends Actor with Logging {
    def act() {
      loop {
        react {
          case msg => logger.info(msg)
        }
      }
    }
  }
  ```
- If structures that return values - Scala's if statement (and for expressions) can return values, which can reduce a little bit of boilerplate (and also replace the odd looking ternary operator from Java).

  In Java:
  ```java
  //the if statement
  int testing1;
  if (somethingBoolean) {
    testing1 = "Hey that was true!";
  } else {
    testing1 = "Darn, that was false.";
  }


  //or the ternary
  int testing2 = somethingBoolean ? "Hey that was true!" : "Darn, that was false.";
  ```

  In Scala:
  ```scala
  //consistently use if structure for if-like things
  val testing = if (somethingBoolean) "Hey, that was true!" else "Darn, that was false."

  //even more useful with implicit return
  def method() = {
    if (somethingBoolean) {
       //...
      testing
    } else {
      //...
      otherTesting
    }
  }
  ```
- For expressions - If I had learned about Scala after Erlang, I might have caught on to this at the time, but for expressions in Scala are very similar to list comprehensions in Erlang (I would even argue more powerful).
  ```scala
  val list = List(1, 2, 3, 4, 5, 6, 7, 8, 9)

  for (x <- list; x <= 4) yield x * 2
  //returns List(2, 4, 6, 8)
  ```
- Implicit return value - In Scala you don't need to explicitly return anything.  The final expression calculated is what is returned.  It actually seems to be considered bad style to use the return keyword.  Groovy has this same feature, and I never really liked it (except in closures).  It seemed confusing that there wasn't a return statement.  However, with a staticly typed language like Scala, I'm seeing the light.  Having the compiler tell you you are returning the wrong type of variable is a lot nicer than not catching it until runtime.
- Option type (i.e. Death to nulls!) - In Java, you have to worry about the dreaded NullPointerException (NPE) since null is the general approach to saying that a variable has no value.  Since there's no way of telling whether a variable might be null or not, you should really be doing null checks all over the place.  Yuck...

  In Scala, however, the idiomatic approach is to use the Option[T] type.  This says that the variable may or may not actually have a value.  It's value will either by Some(value: T) or None.  The Option class has a bunch of nice methods to help you deal with these results:
  ```scala
  def checkValues(map: Map[String, List[Int]]) {
    //calling get on a map returns an Option[V] (V being the type of the values in the map)
    val potato = map.get("potato")

    //can handle with pattern matching
    potato match {
      case Some(list) => list.map(_ * 2).foreach(println) //ooooo... type safety
      case None => println("potato was not set")
    }

    //can provide a default value
    potato getOrElse Nil //Nil is a shortcut for an empty list

    //can use collection operations or for expressions
    potato.map(_.map(_ * 2)) getOrElse Nil
  }
  ```

  Scala does still have null for Java interoperability, but its use is highly discouraged.  If you can still get NPEs, then what's the benefit, you ask?  Using Option gives compile-time enforcement that the developer needs to be aware  there might not be a value for this object.  In Java, you have to rely on the developer reading the Javadoc and then remembering it when they go to use the method.

There are other things I'm having trouble grasping:

- Immutability - I'm so used to the approach of encapsulating mutable state in an object, that it puzzles me to try to write a program without (or with significantly less) mutable state.  Scala lets you use mutable state, but they do nudge you towards immutability.  With mutable state you can pass the object to someone and know that no matter when they decide to use it, they'll have the up to date version.  Granted if you passed it to another thread you have to be worried about concurrency issues.  Using Actors to encapsulate some of the major mutable state has been my approach so far, which seems to be helping.
- Import statements - Scala has much more powerful (shoot yourself in the foot powerful) import statements.  There are a bunch of different flavors:
  ```scala
  //normal import one type import
  import java.net.URI //OK, makes sense

  //everything in the package
  import actors._  //considered bad form in Java, but OK

  //import a few specific types
  import xml.{Node, NodeSeq} //hmm, interesting...

  //rename types
  import collections.mutable.{Map => MutableMap} //whoa

  //relative imports
  import java._  //ok, why?
  import io.File  // stop it
  import util._   //really, this is just crazy

  //absolute imports, if you're scared
  import _root._.java.net.URL
  ```

  The concepts behind these imports aren't confusing and the syntax is straightforward.  My problem is that in Java wildcard imports (import java.util.*) are considered evil because you aren't completely sure which types you are using from which packages.  It makes it a lot harder for someone new to your code to come in and understand what each of the types you use correspond to.

  General practice in Scala is to use the wildcard and relative imports.  Obviously you need to be careful with this because importing everything willy-nilly is just going to cause issues.  There are benefits to this for importing type aliases, case classes, and implicit functions, but it's a big change.
- IDE support - I'm an Eclipse guy.  While Scala does have an Eclipse plugin, it's a little lacking.  I understand that it's a newer language and it's going to take a while for it to catch up but there are some annoyances:
    - Compiler errors don't display if you hover of the snippet underlined in red.  You need to go to the side of screen and hover over the red X.  Time drains away, seconds at a time.
    - Compiler errors are sometimes wrong or missing.  Some compiler errors won't go away but work just fine when I compile with scalac.  There are also things that don't fail in Eclipse that do in scalac.  However, all in all, something is better than nothing, and considering how slow Scala compilation is, something is a good start.
    - Side note: One huge benefit of the IDE is that hovering over a method/variable/expression will tell you what it's qualified type is.  That's a huge benefit with relative imports.

Well, that's enough for one sitting.  I just started playing with Lift a couple days ago, so next post will probably about that.

As a final note: Get Up With It by Miles Davis.  The End.
