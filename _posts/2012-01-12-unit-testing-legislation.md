---
layout: post
title: Unit Testing Legislation
date: 2012-01-12 01:00:00
category: political
---
Just think how cool it would be if you could run unit tests on legislation...

I was just reading through the [Wikipedia page](http://en.wikipedia.org/wiki/Stop_Online_Piracy_Act) on [SOPA](http://thomas.loc.gov/cgi-bin/bdquery/z?d112:h.r.3261:) (the Stop Online Piracy Act), with people going back and forth about whether the bill's language does or does not permit certain activity.  I'm misusing the term unit testing, but the idea of running automated tests against legislation to verify that it fulfills it's intended purpose is very appealing.  It's inherently difficult (more likely impossible) given the way that law works (not that I understand it), but just go with me for a minute.  Imagine if you could write (and run) something like this (yay for [Spock](https://andrew-oberstar.squarespace.com/blog/2012/1/12/spockframework.org)) against SOPA:

```groovy
    class SopaTest extends Specification {
        Sopa sopa = new Sopa()

        def 'sopa stops foreign sites dedicated to piracy'() {
            given:
            Site site = new PiracyRUs()
            Person ownerOfSite = new Pirate()
            ownerOfSite.uploadTo(site).file(entireMovie)
            expect:
            sopa.isSiteInViolation(site)
        }

        def 'sopa does not shutdown youtube'() {
            given:
            Site site = new Youtube()
            Person userA = new OrdinaryPerson()
            userA.uploadTo(site).file(fairUseClip)
            expect:
            !sopa.isSiteInViolation(site)
        }
    }
```

Run that and find out if SOPA really does violate our First Ammendment rights or not.  Just think how easy life could be then.
