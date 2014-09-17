---
layout: posts
title: Creating content with Pandoc and RMarkdown
tags: [Publishing, R]
summary: Authoring rich content including maths and R code from simple markdown
---

I'm used to seeing complex scientific content produced in rather involved formats like XML or LaTeX, but recently I've been looking at tools that allow rich content to be authored in more user-friendly formats like Markdown. I first heard of **RMarkdown** via a [presentation by a guy called Shaun Jackman](http://sjackman.github.io/open-science/#/open-reproducible-science) that I saw on Twitter. Produced by the team at [RStudio](http://www.rstudio.com/), [RMarkdown](http://rmarkdown.rstudio.com/) brings together a bunch of underlying components which enable you to write content in markdown which includes snippets of R code, and then evaluate that code to insert results, tables, charts etc into HTML. PDF or other destination formats.

### Pandoc
The foundation stone of all this is John McFarlane's [Pandoc](http://johnmacfarlane.net/pandoc/index.html), billed as a 'universal document converter' capable of coverting to and from a vast array of text-based file formats.

I installed that as per the instructions on the site and was immediately able to generate documents from markdown thus:

{% highlight bash %}
pandoc hello.md -o hello.html 
pandoc hello.md -o hello.docx 
{% endhighlight %}

In order to make PDFs you need to install a **LaTeX engine**. I didn't want to install a big clunky TeX editor on my Mac, so I used [BasicTex](http://www.tug.org/mactex/morepackages.html). I had to [modify my $PATH](http://oct.tclh123.com/blog/2013/09/09/use-pandoc-and-latex-on-os-x/) to make it work. 

### R

Installing [R itself](http://www.r-project.org/) is quite straightforward. Once you've got it running R has a package management system for installing libraries. I had a slight glitch there in that it seemed to need to open an Xwindow in order for me to manually choose a package mirror, and running OS/X 10.8 meant I needed to [install Xwindowing software first](http://socserv.mcmaster.ca/jfox/Misc/Rcmdr/old-Mac-installation-notes.html). 

I first needed to install the ['devtools'](http://cran.r-project.org/web/packages/devtools/index.html) package, which for some reason turned out to involve downloading the package and [installing it locally from a zip](http://stackoverflow.com/questions/1474081/how-do-i-install-an-r-package-from-source). 

I could then [install RMarkdown](https://github.com/rstudio/rmarkdown) itself using the package management system as you'd expect:

{% highlight r %}
devtools::install_github("rstudio/rmarkdown")
{% endhighlight %}

Ultimately I did all this because I wanted to be all command-liney and not just install the [RStudio application](http://www.rstudio.com/) instead.

### RMarkdown

Stuff about using RMarkdown.

