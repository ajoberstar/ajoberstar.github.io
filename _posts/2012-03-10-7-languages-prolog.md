---
layout: post
title: "7 Languages: Prolog"
guid: 5005ed49e4b0d534734f5630:5005f070e4b0ee36c463b555:5005f070e4b0ee36c463b589
date: 2012-03-10 01:00:00
category: technical
tags:
    - prolog
    - programming languages
    - 7 Languages in 7 Weeks
---
Next up in 7 Languages in 7 Weeks was [Prolog](http://en.wikipedia.org/wiki/Prolog).  This is a logic programming language.  Your "code" defines facts and rules, and then executes queries on them.  It's all declarative, you don't ever see the algorithm that Prolog uses.  It's a very different way of thinking, since you are just describing the problem, and asking Prolog to solve it for you.

One of the challenges was to reverse a list in Prolog.

```prolog
list_reverse([], []).
list_reverse([X], [X]).
list_reverse([Head|Tail], Reversed) :-
    list_reverse(Tail, ReversedTail),
    append(ReversedTail, [Head], Reversed).
```

Here's some explanation of that:

1. The reverse of an empty list is an empty list.
2. The reverse of a one item list of the same one item list.
3. The reverse of a two or more element list is the reversal of elements 2 through the end followed by the first element.

I had a hard time wrapping my head around this approach.  The third set of exercises was solving Sudoku and the 8 Queens problem.  The solution the author showed for a 4x4 solution was interesting, but it seemed way too tedious.

```prolog
valid([]).
valid([Head|Tail]) :-
   fd_all_different(Head),
   valid(Tail).

sudoku(Puzzle, Solution) :-
    Solution = Puzzle,
    Puzzle = [S11, S12, S13, S14,
              S21, S22, S23, S24,
              S31, S32, S33, S34,
              S41, S42, S43, S44],
    fd_domain(Solution, 1, 4),
    Row1 = [S11, S12, S13, S14],
    Row2 = [S21, S22, S23, S24],
    Row3 = [S31, S32, S33, S34],
    Row4 = [S41, S42, S43, S44],
    Column1 = [S11, S21, S31, S41],
    Column2 = [S12, S22, S32, S42],
    Column3 = [S13, S23, S33, S43],
    Column4 = [S14, S24, S34, S44],
    Square1 = [S11, S12, S21, S22],
    Square2 = [S13, S14, S23, S24],
    Square3 = [S31, S32, S41, S42],
    Square4 = [S33, S34, S43, S44],
    valid([Row1, Row2, Row3, Row4,
        Column1, Column2, Column3, Column4,
        Square1, Square2, Square3, Square4]).
```

The exercise was to expand that solution for 6x6 and 9x9.  That would have either meant a lot of typing and no thinking or an extreme amount of thinking trying to generalize a solution.  I just didn't grasp the though process required for Prolog enough to try that.

Prolog has some fascinating use cases.  At the beginning of the chapter, the author interviewed someone who had writting a masters thesis on predicting the behavior of a trained dolphin, given the rules the dolphin was taught. Apparently, Prolog also has a lot of use in natural language processing, with the IBM Watson computer even being partially written in it.

The end result is that Prolog doesn't click for me.  I would need a lot more time with it, than I want to spend.  Especially considering I don't see any direct use cases for Prolog in the stuff I like to play around with.

Next up is Scala.
