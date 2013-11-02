---
layout: posts
title: Ruby and XSLT using Nokogiri
tags: [Ruby]
summary: How to apply an XSLT transform using Nokogiri.
---

I may be an old-fashioned kind of guy but for certain types of job I still don’t think there’s an easier way to process XML than using a bit of XSLT. When I googled for a solution I initially encountered some pretty outdated stuff which went too deeply into core Ruby XML libraries. But it turns out to be easy.

Using the [Nokogiri](http://nokogiri.org/) gem:

{% highlight ruby %}
#!/usr/bin/env ruby
# encoding: UTF-8

require 'nokogiri'

doc = Nokogiri::XML(File.read('myxmlfile.xml'))
xslt = Nokogiri::XSLT(File.read('myxslfile.xsl'))

puts xslt.transform(doc)
{% endhighlight %}