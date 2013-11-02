---
layout: posts
title: Designing a site 'mobile first'
tags: [Mobile, Design]
summary: Designing the front end of a website by starting with the limitations of a small mobile screen and then enhancing up for larger screens turns out to be a simplifying and liberating experience.
---

*Designing the front end of a website by starting with the limitations of a small mobile screen and then enhancing up for larger screens turns out to be a simplifying and liberating experience.*

I’d heard the buzzphrase ‘mobile first’ a few times, not least from the UI guys at work, but I wasn’t sure that designing a website to work on mobile browsers before making it work on desktops was really sensible given that mobile still often constitutes only a small proportion of overall traffic. However the other day I set about making a simple static site for a friend’s business, and I thought it was important that it should work well on a phone. I started with a pretty standard fixed-width template downloaded from the web and then tried retrofitting some basic mobile support to it, but it didn’t feel very satisfactory, much like my initial attempt to mobile-ise this site. So I thought I’d try starting again mobile first.

My approach was cribbed from the [HTML5 Rocks](http://bit.ly/SZiA3T) site. I had two stylesheets, one called ‘basic.css’ intended to be loaded by all browsers, and then one called ‘enhanced.css’ loaded by a media query when the window was wider than yay big or when using an older version of IE:

{% highlight html %}
<link rel="stylesheet" type="text/css" href="basic.css" media="screen, handheld" />
<link rel="stylesheet" type="text/css" href="enhanced.css" 
media="screen and (min-width: 640px)" />
<!--[if (lt IE 9)&(!IEMobile)]>
<link rel="stylesheet" type="text/css" href="enhanced.css" />
<![endif]-->
{% endhighlight %}

I’d taken my cue from our developers at work in using a pixel-based rather than a relative breakpoint, it just seemed simpler given that I had a couple of images and things to scale on the site. The ‘enhanced’ layout would apply when the browser window was wider than 640px, which meant that the ‘basic’ layout would be seen on a phone in either orientation. The enhanced layout should work fine on an iPad in landscape, at this point I’m not too bothered about how it looks in portrait.

To start coding I simply narrowed my browser to below the breakpoint, pointed my phone browser at the local IP of my machine and set to work. And this is where it got a lot easier. With that narrow window there were few decisions to make - no columns, no floats, no positioning, just one thing below another.

The basic css contained a reset and set colours and type, which was relatively sized using ems. After that all I really needed to do was to set some padding and margins between each block of the content. There wasn’t much content so I didn’t need to worry about overall scroll length or use any fancy JS to fold pieces away. With so little to do it all came together very quickly and satisfyingly.

![Illustration](/assets/images/posts/mobilelayout.png)

Having arrived at a decent looking phone experience I then turned my attention to what happens when the browser width scrolls out beyond the 640px breakpoint by adding styles to enhanced.css. This was mainly a matter of resorting the different bits of the content into a fluid two-column layout by adding some floats and some max-widths. I wanted to add a decorative image to the full-screen design so I took the easy way out and just hid it in the basic layout - not ideal as it still has to be loaded, but it’ll do for now. I did some similar toggling of the display property for a couple of minor navigational elements on the site and that was about it - the enhanced css file was remarkably short.

When compared to my previous efforts at retrospective mobile optimisation this entire process felt cleaner, simpler and more reliable. But the real thing that surprised me was that it also felt better than designing a regular desktop-optimised site - starting with the small, narrow screen limited my options and concentrated my thought processes, while splitting between ‘basic’ and ‘enhanced’ css seemed to produce better and more logically organised code. I think this will become my default way of working from now on.

