---
layout: posts
title: Custom Haml filters in a Sinatra application
tags: [Ruby]
summary: 
---

I've been working on a little ruby/sinatra application which involves displaying content rendered from quite a complex proprietary XML format. I decided to use [Haml](http://haml.info/) as my templating engine for rendering the views, and added a custom filter to turn the proprietary content into XML. Here's how they work.

Haml uses [filters](http://haml.info/docs/yardoc/file.REFERENCE.html#filters ) to transform foreign markup in a view. For example:

{% highlight ruby%}
%p
  :markdown
    Lorem ipsum *dolor* sit amet
{% endhighlight %}

renders as

{% highlight html%}
<p>Lorem ipsum <em>dolor</em> sit amet</p>
{% endhighlight %}


By default the Haml gem includes filters for dealing with common markup types like markdown or coffee script. But if you're working with some other type of non-standard markup then you can add your own custom filter to process it. 

Imagine that your markup format looks like this - for convenience I'll call it 'Pipemark':

{% highlight html%}
Lorem ipsum |boldface|dolor|end boldface| sit amet,
consectetur |boldface|adipisicing|end boldface| elit
{% endhighlight %}

You make a custom filter by building on top of the [Haml base filter class](http://haml.info/docs/yardoc/Haml/Filters/Base.html). Your filter needs to have a **render** method for converting the markup into HTML. For 'Pipemark' that's just a simple substitution:

{% highlight ruby%}
module Haml::Filters::Pipemark
  include Haml::Filters::Base
 
  def render(input)
    output = input.gsub(/\|boldface\|(.*?)\|end boldface\|/,
                       '<strong>\1</strong>')
  end
 
end
{% endhighlight %}

Pass a bit of 'Pipemark' data to your view, e.g. for my Sinatra app:

{% highlight ruby%}
get '/example' do
  data = "Lorem ipsum |boldface|dolor|end boldface| sit amet, 
          consectetur |boldface|adipisicing|end boldface| elit"
  haml :example, :locals => {:quote => data}
end
{% endhighlight %}

To render it all you have to do is invoke this filter in your Haml template with a colon:

{% highlight haml%}
%div
  :pipemark
    #{quote}
{% endhighlight %}
 
which produces

{% highlight html%}
<div>Lorem ipsum <strong>dolor</strong> sit amet, 
	consectetur <strong>adipisicing</strong> elit</div> 
{% endhighlight %}

The render method in my actual example used some xslt to transform xml into html, but the principle was the same.