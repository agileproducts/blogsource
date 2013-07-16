---
layout: posts
title: A Scanty blog
tags: Ruby Scanty_blog
---

On previous occasions when I’ve played around with blogs I’ve generally used Wordpress, but of late I’ve become a bit tired of it. I can never seem to find a theme I like and waste ages trying to create my own or to reverse engineer some unintelligible off-the-shelf PHP. Since I’m trying to learn Ruby I thought that perhaps this time I should look for a Ruby blogging platform.

Googling found a few, but the one that attracted me was [Scanty](https://github.com/adamwiggins/scanty) by Adam Wiggins. As he [describes it](http://adam.heroku.com/past/2008/11/4/scanty_the_blog_thats_almost_nothing/) it’s a very, very minimal system - and therefore ideal for a beginner, there’s only a small amount of simple code to pick apart.

The code doesn’t appear to be being maintained and I had a few issues getting it working. First of all I had to fix the [compatibility issue](https://github.com/adamwiggins/scanty/pull/4) with newer version of Sinatra and for a while didn’t realise that I needed to add a Gemfile to get it running on Heroku. Then when I tried to save my first post it chucked an error which seemed to trace back to one of the vendored gems and was to do with parsing or encoding. At that point I was running Ruby 1.8.7 locally, and I decided the only thing for it was to upgrade to 1.9.2 and replace the vendored gems with the latest versions as part of my bundle.

But now here we are, it’s working. Let’s see how we get on.