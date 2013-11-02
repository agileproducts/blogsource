---
layout: posts
title: The Google Analytics API and Ruby
tags: [Ruby, Analytics]
summary: Mechanically retrieving data from Google Analytics.
---

*Getting data from the Google Analytics API using the Garb gem*

We wanted to get a list of the top 50,000 search terms that resulted in a referral from Google to the main site for the company where I’m currently working. Trying to obtain them via the regular browser interface was painful, so we looked at using the API instead.

I looked for a bit of Ruby to help, and sure enough I came across [Garb](https://github.com/vigetlabs/garb), an handy little gem which makes talking to Google very easy indeed.

Here’s what my script looked like:

{% highlight ruby %}
#!/usr/bin/env ruby
# encoding: UTF-8

require 'garb'

#Set up the connection
Garb::Session.login('mygoogleusername', 'mypassword', :account_type => "GOOGLE")

profile = Garb::Management::Profile.all.detect {
  |profiles| profiles.web_property_id == 'UA-myid'}

#Define which statistics are wanted
class GoogleSearches
  extend Garb::Model
  metrics :visits
  dimensions :keyword
end

#You can only fetch 10,000 results at a time from the API
#So I had to break this into five pieces
(0..4).each do |i|
  iterator = i.to_s
  
  resultset = GoogleSearches.results(
    profile, 
    :limit => 10000,
    :offset => (i*10000)+1,
    :start_date =>  Date.today - 180,
    :end_date => Date.today,
    :filters => {:source.contains => 'google'},
    :sort => :visits.desc
  )

  #Write the results in a csv file, 
  #stripping out any commas in the search terms themselves
  open('googleterms'+iterator+'.csv', 'w:UTF-8') do |f|
    resultset.each do |row|
      f.puts row.keyword.gsub(/,/u,' ') + "," + row.visits
    end

  end
end

{% endhighlight %}

The main thing I had to watch for was character encoding, in the case it was important to preserve all the UTF8 encodings in the search terms, many of which weren’t in English. My Windows 7 machine at work gave me lots of trouble here, to no great surprise it wasn’t an issue when I tried using it on my Mac at home.