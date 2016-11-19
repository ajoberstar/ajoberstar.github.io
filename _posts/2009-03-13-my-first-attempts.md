---
layout: post
title: My First Attempts
category: technical
date: 2009-03-13 01:00:00
tags:
  - netflix prize
---
I'll preface this by saying I have no hopes, expectations, or anything else of actually competing in this prize.  I came into this hoping to learn about recommender systems.

So I started by finding some research papers on recommender systems and collaborative filtering.  I read that and assumed I could start implementing a nearest neighbor algorithm.  So I pulled out my trusty old Java and wrote a quick app to import the training set into a MySQL database.  Once the import actually started to work, it took 10 hours to import.  Once that happened some reality set in as to how massive this was compared to anything I'd worked on before.  Little did I know, I still hadn't learned.

Then I started to implement my nearest neighbor algorithm.  After working on that off and on for a week or so, I ran it.  5 hours later it was still calculating similarity scores for the first prediction. With another 1.5 million ratings to predict that it hadn't even started on, I realized this was pointless.  So a trip to the Netflix forum and I realize that nobody in their right mind is running their algorithms from a database. After putzing around on my own for a while trying to figure it out.  I found a Java framework which I proceeded to modify to my heart's content to get it all to run in memory.

Now that I felt like this could start working I modified my nearest neighbor algorithm to work with the memory backend, but yet again it was taking way too long.  8000 out of 1.5 million in 12 hours.  Another trip to the forum and my mistaken assumption from the papers I had read that nearest neighbor was the best algorithm to start with was highly faulty.  On to matrix factorization...
