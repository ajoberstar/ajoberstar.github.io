---
layout: post
title: Don't Rush Your Math
category: technical
tags:
  - netflix prize
  - matrix factorization
---
I've been trying to implement Gravity's BRISMF#250 model but have been getting much higher RMSEs.  I had no idea what was wrong so I decided to move on and start implementing the code to retrain features after the initial training.  To test I had to rerun my BRISMF#1 model which resulted in an RMSE 0.01 higher, which made no sense.  I looked through my code for changes I've made since I initially ran that and came across an error.

Most algorithms will require different ranges of random values to fill the feature arrays.  But, the way Java's random double generator is set up, it will only return a value between 0.0 and 1.0. Since that's not going to be helpful, I made a quick equation to modify the range. Unfortunately I rushed through what should have been a simple equation and came up with the following.

    value = randomDouble * (max - min) - min;

The problem with this is if you wanted a range between -0.01 and 0.01, you end up with one between 0.02 and 0.03.  It should have been:

    value = randomDouble * (max - min) + min;

Now that I've fixed this I can try BRISMF#250 again.  Lesson learned: don't rush your math (even really simple math).
