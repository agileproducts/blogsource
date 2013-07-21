---
layout: posts
title: A tag-list for my Scanty blog
tags: Ruby Scanty_blog
summary: Adding a taglist to the Scanty framework.
---

One feature I’ve been missing from Scanty is a tag-list or cloud - for me that’s always an easy way to see what a blog site is about. But it wasn’t too difficult to make one. I defined a helper method in Sinatra like this:

{% highlight ruby %}
#gets all the tags and returns them as uniqued hash with freq count

def get_taglist 
#select tag from posts table and put into an array
#e.g. ["Ruby Analytics", "Ruby XML"]		
  rawtaglist = Post.select_map(:tags)
		
  #split compound values into new array of discrete tags
  #e.g. ["Ruby", "Analytics", "Ruby", "XML"]
  tag_array = Array.new
  rawtaglist.each do |rawtag|
    temparray = rawtag.split
    temparray.each do |i|
      tag_array << i
    end
  end
		
  #Gather like values together in a hash
  #e.g. ["Ruby" => ["Ruby, Ruby"], "Analytics" => ["Analytics"], "XML" => ["XML"]]
  temp_hash = tag_array.group_by {|value| value}
		
  #Build a new hash of key=>values_array.length
  #E.g. ["Ruby" => 2, "Analytics" => 1, "XML" => 1]
  tag_hash = temp_hash.inject({}) do |result, element|
    result[element.first] = element.last.length
    result
  end
		
  #return hash sorted by count value
    tag_hash.sort_by {|key,value| value}.reverse
end

{% endhighlight %}

and then got the taglist in each page route and passed it to the view like this:

{% highlight ruby %}
get '/past' do
  posts = Post.reverse_order(:created_at)
  taglist = get_taglist
  @title = Blog.sitetitle + " | Archive"
  erb :archive, :locals => { :posts => posts, 
	                     :taglist => taglist, 
	                     :navhighlight => 'blog'}
end
{% endhighlight %}

The ultra-simple schema behind Scanty isn’t ideal for this purpose because if you assign multiple tags to a post it’s all stored as just one long string, which is why I need to do all that messing around sorting and splitting arrays. I can’t believe it’s particularly efficient and at some point I probably need to bite the bullet and alter the database. But still, I learned a little about things like the Ruby [inject](http://blog.jayfields.com/2008/03/ruby-inject.html) method and it all appears to work well at the moment - in proper agile fashion it is just enough to do the job.