---
layout: post
title: Progress Without Perfection
category: technical
tags:
  - netflix prize
  - matrix factorization
---
Initially, I thought that given the nice detail in the Gravity team's papers, I would be able to implement these and get very close scores. It has turned out not to be the case. As the models get bigger and more complex my results have moved farther away from theirs: not terribly far, but far enough. This could be a factor of details they didn't include in the papers, details I missed in the papers, or my misinterpretations (or programming errors) in implementing them.

This was irritating me last week, because I didn't really want to move on to the next level of the algorithm until I had gotten the previous one working. But now I've given up on that. Even though I am not as close to their results as I would like, I am making progress and now with my implementation of their 250 feature, retrained model BRISMF#250UM I have a quiz score of 0.8967.

The idea behind the retraining is that as the model adjusts features, the users at the end of the list are being adjusted against different movie features as the top of the list. This is because everything is trained simultaneously. The retraining as initially conceived by the Gravity team, was to reset the user features and lock in the move features. Thus, when training again users are adjusted against fixed movie features, hopefully for better results. But they ended up finding better results by not just retraining the now reset user features, they also continue to train the movie features from the original run. This ended up with much better results, and is how I got the 0.8967.

What I was doing today was adding in the neighborhood based correction to the predictions. I spent a long time looking at the formula, because I didn't really get it, but I think this is what the idea is.

In general, a neighborhood based (NB) approach uses the ratings of other users to determine what you would rate something. Since some users are more like you than others, contributions are weighted depending upon the similarity between the 2 of you, which can be determined in various ways.

In specific to Gravity's NB correction, some portion of the predicted error is added on to the regular MF prediction. The predicted error is found via a NB algorithm. Essentially you look in the training set (the ratings you have the answers for) and find what the error of each other rating by that user is. These are combined based on similarity weights again, to make similar items (in the case of Gravity's paper) contribute more to the projected error.

I'm still working on how to determine the parameters for the correction, but it looks like it could be promising.
