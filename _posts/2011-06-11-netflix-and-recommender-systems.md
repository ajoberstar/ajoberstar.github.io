---
layout: post
title: Netflix and Recommender Systems
category: technical
tags:
  - netflix prize
---
This was written as a speech for a training class at work, so the tone is a little odd for a blog post, but oh well.

> Gary, Sue, and 10 other people like this comment. Customers who shopped for this chair also shopped for that CD.  Our best guess for you is 3.7 stars. Many sites now recommend things to you based on the way you use their site. But why do they need to do this?  You can find anything on the Internet.  But, because everything is at your fingertips, there's an information overload.  There's no way I can look through every movie Netflix has and find the one I should watch next.  In order to help us navigate all of these choices, and ultimately become loyal paying customers, websites need to provide value by showing us things we will like.
>
> Most sites today that have user ratings information will still merely show you a basic average of everyone's opinion.  Based on the number of ratings, this will either tell you what the entire world thinks of something (if it's popular), or what some cult following thinks of it.  Neither of which is necessarily applicable to you. What you would rather know is what people who have similar tastes think of it.
>
> For my senior research project, I looked at recommender systems; specifically in the context of the Netflix Prize.  The goal of this contest was to improve on Netflix's recommendation algorithm by 10%, for which they would award $1 million. They released a massive dataset of 100 million ratings from around a half-million users across a total of 18,000 movies.
>
> Through my research I found that there are many different approaches to recommender systems. I'll just cover one that's a little easier to visualize, called matrix factorization.  I'll skip the gory math details, but essentially what it tries to do is detect common features among movies. You can think of a feature as action, comedy, or romance, but it ends up being more abstract than that since the algorithm doesn't understand those concepts, it just sees a common thread in the data.  For a particular feature, it will try to estimate how much a movie exhibits each of those features and how much a user likes a particular feature. The algorithm will take all of these features together to make its prediction.
>
> What you ultimately want get out of these recommender systems, is the ability to take advantage of all of the variety these services provide, but not have to do the dirty work yourself.  You can leverage recommendations based on your own preferences, to ideally find movies that you might not have find on a best-seller list, but may just be your favorite movie that you never knew existed.
