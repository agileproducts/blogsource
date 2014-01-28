---
layout: posts
title: Using Twilio to send emails via an SMS message
tags: [Ruby, Mobile]
summary: Building myself a secretary
---

*Building myself a secretary*


The other day I was severely delayed coming into work on the train. Not for the first time I found myself wishing I could use my phone to email to our office mailing group apologising for my tardy appearance. Erm, I know phones can send emails now, right? Well yes, *if* you have a data plan. But I'm a cheapskate and run my phone pay-as-you-go, which means that I'm quite reluctant to switch 3G data on. What I want to do is send an email triggered by a cheap and cheerful SMS message. My provider won't let me do that - so I made myself a secretary.

[Twilio](https://www.twilio.com) is a cloud service which provide a simple mobile telephony API. You sign up for a phone number which costs $1 a month, and then configure that number so that when it receives a voice call or sms it either gets or posts data about the incoming message as parameters to an endpoint:

![Illustration](/assets/images/posts/twilio.png)

For an SMS message the [posted or gotten data](https://www.twilio.com/docs/api/twiml/sms/twilio_request) includes things like the phone number the message was sent from and the body of the message.

When the endpoint is hit it needs to return response to Twilio telling it what (if anything) to do about the message it has received. This response is in an XML-based format called [TwiML](http://www.twilio.com/docs/api/twiml). The [response](https://www.twilio.com/docs/api/twiml/sms/your_response) to an incoming SMS sent by Twilio's sample default endpoint looks a bit like this:

{% highlight ruby %}
<?xml version="1.0" encoding="UTF-8"?>
<Response>
  <Message>Thanks for your text!</Message>
</Response>
{% endhighlight %}


Which will make your Twilio number text you back with the contents of the Message element.

In my case I didn't want Twilio to respond to my incoming message. I pointed the SMS handler for my number at a simple Sinatra app hosted on Heroku which returned an empty response:

{% highlight ruby %}
<?xml version="1.0" encoding="UTF-8"?>
<Response></Response>
{% endhighlight %}


What I *did* want my Sinatra app to do is send me an email with the contents of the SMS. For this I just hooked up the [Postmark](https://postmarkapp.com/) add-on in Heroku. For my first iteration I just took the 'body' parameter of the incoming post and emailed the lot to an address that was hardcoded in. But then to make it a bit more flexible I introduced a format which could parse the destination address from the SMS body like thus:

{% highlight ruby %}
destination@mail.com|Here's my message!
{% endhighlight %}

{% highlight ruby %}
text_message = params["Body"]

mail_message = Mail.new do
  from            "registered@fromaddress.com"
  to              text_message.split('|')[0]
  subject         "A message from my secretary"
  body            text_message.split('|')[1]

  delivery_method Mail::Postmark, :api_key => ENV['POSTMARK_API_KEY']
end

mail_message.deliver

{% endhighlight %}

I might take this further, adding shortcodes for known email addresses like:

{% highlight ruby %}
teammail|Sorry guys, I'll be late for the meeting
{% endhighlight %}

Or enable my secretary to do things other than email:

{% highlight ruby %}
tweet|I could send tweets by SMS!
{% endhighlight %}

Who knows? At less than $1c to receive an SMS (about $4c to send one) my secretary will be cheaper than 3G data. But of course that's not really the point. Being able to develop apps which use the phone network is fun, and while their documentation could use some work Twilio is easy to use and a good place to start.
