---
layout: post
title: Gradle > Sliced Bread
category: technical
tags:
    - gradle
    - build
---
I'm not really convinced that sliced bread is that much of an improvement over uncut bread, but Gradle is definitely better. Considering how much I've been using [Gradle](http://gradle.org) over the last 2 years, I'm surprised I haven't written anything about it yet.

Let's start with the basics. Gradle is a build automation tool, primarily supporting JVM languages (e.g. Java, Groovy, Scala). You may be familiar with Ant and Maven, the two previous behemoths in the Java build space, but for those who don't know:

* [Ant](http://ant.apache.org/) is an XML based tool. You write a build file listing out all of the tasks you want to run. Once you have a build file set up, it's pretty good. Unfortunately, you need to define every action it will take and wire all of the inputs and outputs together. Also, if you realize that all of your JAR build scripts look the same, you're not going to have a very easy time trying to reuse that logic.
* [Maven](http://maven.apache.org/) took the opposite philosophy of Ant. Rather than being a toolkit that you could do with what you please, Maven is based on the idea that everything is essentially built the same. Your XML file, is no longer a true build script, defining your actions, but instead a descriptor explaining what your project is. Maven is entirely declarative and all projects are supposed to use the same convention. All great, until you need to stray from that convention or want one little bit of extra functionality.

Gradle comes in with the benefit of seeing the success and failures of both Ant and Maven ending up with a philosophy of starting declarative, but giving you the option to easily throw in extra logic as needed.

I'm not going to bother with simple examples, since you can easily find beginner tutorials on Gradle's website and elsewhere. This post can at least serve as a high-level introduction to why you might want to look at Gradle and, hopefully, I will be posting some more on this topic in the future.
