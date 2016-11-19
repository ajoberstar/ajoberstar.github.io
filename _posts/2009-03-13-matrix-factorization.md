---
layout: post
title: Matrix Factorization
category: technical
date: 2009-03-13 03:00:00
tags:
  - netflix prize
  - matrix factorization
---
The idea behind matrix factorization (which is similar if not the same as what the Netflix community is calling SVD, singular vector decomposition or something) is that you can estimate an I x J matrix R (the ratings matrix) by multiplying two smaller matrices: an I x K and a K x J.  Each of those K rows/columns is known as a feature and the matrix factorization (MF) algorithm will estimate the scores for each user and movie.

What this allows you to do is essentially generate scores for how much action, comedy, romance, etc. is in a movie.  And also how much a certain user likes those aspects.

So I am using the papers written by the Gravity team to try this out.  They've outlined it really well, down to actually giving you the algorithm in psuedocode and listing different parameters they've tried.

So I started working on this and eventually got it to run.  But the algorithm that they say takes 13 epochs (loop cycles, essentially), took mine about 50 with the same parameters.  So now I'm trying to resort the data by date as they have to see if that will work.  But since that took me all day yesterday I decided to submit a prediction from the features I had built before.  It got a 1.0041 RMSE on the quiz set, which is not good.  

Just to give you an idea: Cinematch (Netflix's algorithm) gets a .9514, and the leader (Pragmatic Theory, as of today) has a .8597.
