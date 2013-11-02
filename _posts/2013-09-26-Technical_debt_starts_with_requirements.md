---
layout: posts
title: Technical debt starts with the requirements
tags: [Product development, Business analysis]
summary: Technical debt often originates in over-complex requirements and the product owners should help the developers by striving for simple solutions and being prepared to refactor or retire features that aren't working.
---

*Technical debt often originates in over-complex requirements and the product owners should help the developers by striving for simple solutions and being prepared to refactor or retire features that aren't working.*

It's probably inevitable that every project will go through stages where you find yourselves spending a lot of time taking about [technical debt](http://martinfowler.com/bliki/TechnicalDebt.html), and in our office we're in one of those right now. All the usual reasons  - we're a couple of years into our main product, we took some deliberate shortcuts for commercial reasons, the codebase has gotten bigger, we didn't know then what we know now, etcetera. 

Most of the work we're doing to address the situation is purely technical, but I feel it's important to remember that debt is also a problem for the product and that the product team are part of the solution. You often find that the flakiest and most troublesome bits of code are those which were built to support the most complex and confused features, and the tests which fail most often are those around the most peripheral and ill-used features.

A period when you're focusing on the repayment of tech debt is a great opportunity to review the product, look at what features are and aren't earning their place and redesign or kill those that aren't. The other day I found a page on one of our sites that was averaging less than 5 visits a month. Do we need that feature? Is that code adding any value? Seems unlikely. Drop the feature and there's another bit of build time shaved off.  

I think there's also an important lesson here when it comes to designing new features. If a story feels tight and logical then the code which drives it will probably end up that way too. If a feature starts to become very complex with lots of conditions and edge cases then it's going to be more difficult to implement - more code, more tests, more corners to attract dust. 

As a general rule of thumb, simple requirements lead to simple code and a better product. Complex requirements aren't always avoidable, but they should be challenged to justify themselves. 
