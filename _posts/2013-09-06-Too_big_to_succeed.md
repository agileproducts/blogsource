---
layout: posts
title: Too big to succeed
tags: [Agile, Project management]
summary: The failure of the government’s ambitious Universal Credit system proves the old truth that the way to succeed at very large IT projects is to avoid doing them.
---

*The failure of the government’s ambitious Universal Credit system proves the old truth that the way to succeed at very large IT projects is to avoid doing them.*

If a bad workman blames his tools, then I’m not sure what we should make of Work and Pensions Secretary Iain Duncan Smith. He took to the airwaves the other day to lay the blame for the findings of a devastating [National Audit Office  report](http://www.nao.org.uk/report/universal-credit-early-progress/) into the implementation of his flagship Universal Credit at [everyone’s door except his own](http://www.theguardian.com/politics/2013/sep/05/universal-credit-iain-duncan-smith). As a glance at my Twitter feed could tell you I’m not a great fan of IDS or his party, but in this case I’m more interested in the technical aspects of the project and why it has apparently gone so badly wrong.

Politics aside the basic idea behind UC seems sensible enough - take a multiplicity of different overlapping benefits and streamline them into one coherent payment. Of course that implies doing the same to all the backoffice systems that support them - and again, that seems sensible enough, unless you believe that the government should still run on abacuses and bits of paper. 

The problem comes with the scale of the task that involves - initially costed at a cool £2.4 billion. That’s about 100 times larger than any project I’ve ever worked on. It’s also extremely high-risk, both for the people who depend on prompt and accurate payment of their benefits and for the politicians whose political careers depend upon the success of the scheme. 

So how do you build a £2.4Bn piece of software? Well it appears that the powers-that-be had learnt at least one thing from the litany of past high-profile IT failures. Whitehall have finally received the memo - Waterfall doesn’t work. So they decided that Universal Credit would be an agile project. 

So how do you carry out a £2.4Bn agile project? The answer of course is that you can’t. At the heart of the agile philosophy lies the acknowledgement that in software development you can only see so far ahead. You proceed from one manageable objective to the next, see where it takes you and then revise your plans based on what you have learned. Unfortunately that doesn’t fit too well with a desire to achieve an extremely ambitious fixed objective by a fixed date determined by the electoral cycle, and oh, for a fixed cost as well. 

As this excellent [post-mortem in Computer Weekly](http://www.computerweekly.com/news/2240187478/Why-agile-development-failed-for-Universal-Credit) reports, the end result here was that the Universal Credit project was never really agile to begin with. Gigantic fixed contracts were awarded to the familiar suspects like Accenture and IBM. An agile gloss was applied to what were still essentially waterfall methods. Attempts to recruit smaller suppliers who were familiar with agile methods led to predictable failure and frustration. In response to problems the DWP introduced the shudder-inducing concept of *"Agile 2.0 - a hybrid approach which tried to combine elements of agile and traditional approaches to IT programme management"*. It all sounds like a total train wreck. 

So what’s the answer for these type of big public sector technology projects? It can’t be to simply go back to using waterfall methods, which have been tried and found wanting again and again and again. But nor can it be to simply ‘do agile properly’, as a few of the more starry-eyed zealots would probably argue. You couldn’t have succeeded with this project if you’d simply employed different contractors or followed the letter of the agile manifesto. The conclusion has to be that we should avoid taking on such unmanageably large projects in the first place. As one of the quotes in the CW article puts it *"If Universal Credit was agile.. it would have started with a modest £250,000 budget and evolved from there."* 

Of course that’s easier said than done. It would require a consistent, evolutionary investment strategy to be applied independently of the swings of democratic politics. It would require a significant cultural change to a Whitehall establishment that is probably the antithesis of a successful software development organisation, and it would face serious challenges in trying to resolve the entirely understandable requirement for public expenditure to be transparently bid and accounted for with the need to attract new and smaller suppliers who can’t afford the paperwork. 

The recent success of the new [.gov.uk](https://www.gov.uk/) website proves that in the right circumstances it _can_ be done. But I suppose if I really knew the answer, I wouldn’t be sitting here writing this.