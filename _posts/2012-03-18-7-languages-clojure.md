---
layout: post
title: "7 Languages: Clojure"
date: 2012-03-18 01:00:00
category: technical
tags:
    - clojure
    - programming languages
    - 7 Languages in 7 Weeks
---
Oooooo....  [Clojure](http://en.wikipedia.org/wiki/Clojure).  Along with Scala, this was one of my most anticipated languages (mainly because of the JVM integration).  Clojure is a dialect of Lisp, which is a very old family of programming languages.  Most of the syntax is just parentheses.

For the [xkcd](http://xkcd.com/297/) fans:

![xkcd](http://imgs.xkcd.com/comics/lisp_cycles.png)

I've wanted to try a Lisp for a while and Clojure seems like the most practical one.  Clojure is another functional language, though it's not considered "pure" since it does allow some side-effects.  As I said above, the syntax pretty much just parantheses grounping function calls.

```clojure
;; create a list of numbers
(list 1 2 3 4 5)
;; define a value
(def stuff (list 1 2 3))
;; prefix notation
(+ 1 2)
;; map function that doubles each element in the list
(map #(* 2 %) stuff)
```

Beyond trying to mentally parse all of those parens, the prefix notation can get a little confusing.  Instead of saying `(1 + 2)` you have to say `(+ 1 2)`.  In Io you passed a message to an object. In Clojure you pass arguments to a function.  Even things like if statements have been turned into functions.

```clojure
(if (= 3 (count stuff))
  (println "If is a function!")
  (println "That should have worked."))
```

Another cool thing about Lisps in general is that everything is essentially a list.  The code is data and the data is code.  You can write macros that allow you to create new language constructs:

```clojure
(defmacro unless
  [test body else]
  (list 'if (list 'not test) body else))
```

Clojure also has a strong concurrency focus.  While, as with most functional languages, you should try to stick with immutability, you can still use mutable state in a safe way.  Clojure implements a thing they call Software Transactional Memory (STM), which is basically the equivalent of a database transaction for your application's objects in memory.

There's a lot of cool concurrency stuff in Clojure, but I don't understand it well enough to summarize it.

Clojure is really fascinating.  It's a very different way of programming, but one that didn't crush my head into pulp like Prolog did.  I'm looking forward to playing around with this language more in the future.

One final installment to come: Haskell.
