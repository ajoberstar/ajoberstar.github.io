---
layout: post
title: Things I've Learned About Java
category: technical
date: 2009-03-13 02:00:00
tags:
  - netflix prize
---
Doing a project with this scale of data (100 million ratings, by 480189 users, on 17770 movies) shows a person just how much they don't know about programming yet.

Here's a few things I've learned so far:

1. Objects take up a crap ton of memory.  
   You don't realize this when you're just making you're little Person objects in class, but when you try and fit 100 million ratings in memory, objects are not your friend.  It's all about arrays of primitive types.
2. Integers take up way too much space.  
   Even the relatively small, programmer abused int type will make you cry when you try to do this.  Had to use short for movie ids and byte for ratings.  
3. Doubles are stupid.
   I never knew this but double math in Java is really imprecise.  I don't have much choice (both speed and memory wise) but to use them, but adding simple decimals comes out really goofy.  Google "java double arithmetic" and see the madness.

4. Java does not pass by reference.
   It passes references by value.  (I had heard this before but never ran into a problem with it until now) You may say, "What the heck does that mean?"  Well, for example take a Dog object called fido and pass it to a method that takes a Dog parameter.  Let's say it's called goofy in the method.  Right now fido and goofy point to the same thing.  If you change something in the goofy object it will change the same thing in the fido object, because they're the same object.  But if you say goofy = new Dog();  or goofy = null they no longer point to the same thing.  fido still points where it did but no goofy points to something else.

   That doesn't seem like too much of a problem, but... I had an array of 48000 PrintWriter objects as I was trying to reorganize the data.  At the end of each run I used  a for each (for(PrintWriter print : outputArray)) to set them all to null, so they could be reused in the next run.  But since each element in that array was set into a newly declared print variable, setting print = null didn't set outputArray[i] = null.  So a wasted hour or two of running the sorting program.

That's all I have for now, but I'm sure I'll be posting about this again.
