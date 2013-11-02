---
layout: posts
title: Calculating h-indexes using Ruby
tags: [Ruby, Publishing]
summary: Calculating citation h-indexes using Ruby.
---

*Calculating citation h-indexes using Ruby*

The [h-index](http://en.wikipedia.org/wiki/H-index) is a way to measure the relative importance of a scholarly author or journal based on the number of citations each of their articles has garnered. I wanted to calculate some h-indexes using citation data we had at work and compare the results with those reported by [Google Scholar](http://scholar.google.co.uk/intl/en/scholar/metrics.html#metrics). In order to do this I wrote a little ruby class, so I thought I might as well share it on [github](https://github.com/agileproducts/h-index).