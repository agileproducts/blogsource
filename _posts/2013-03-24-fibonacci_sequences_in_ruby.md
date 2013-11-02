---
layout: posts
title: Fibonacci sequences in Ruby
tags: [Ruby, Maths]
summary: Generating the Fibonacci sequence and testing if a given number is a Fibonacci number in Ruby. Inspired by my attempt at Project Euler problem 2.
---

*Generating the Fibonacci sequence and testing if a given number is a Fibonacci number in Ruby. Inspired by my attempt at Project Euler problem 2.*

I’ve been playing around with trying to solve some of the [Project Euler](http://projecteuler.net/) problems in Ruby. [Problem 2](http://projecteuler.net/problem=2) is all about the Fibonacci sequence. I won’t post my exact answer here (plenty of people have) but I did learn some interesting ruby while working on it. 

The [Fibonacci sequence](http://en.wikipedia.org/wiki/Fibonacci_number) begins:

<div class="maths">
0, 1, 1, 3, 5, 8, 13, 21, 34, 55, 89, 144...
</div>

Each term in the sequence is the sum of the previous two terms:

<div class="maths">
next term = current term + previous term<br/>
F<sub>n+1</sub> = F<sub>n</sub> + F<sub>n-1</sub>
</div>

To start you need to seed the sequence with the first two terms 0 and 1.

Here was my first attempt at a function to generate the first n terms:

{% highlight ruby %}
def fibonacci(n)
  sequence = [0,1]
  (1..n-2).each {|x| sequence.push(sequence[x] + sequence[x-1])}
  sequence
end
{% endhighlight %}

I used a variation on this to find the fibonacci terms smaller than 4,000,000 and thus solve Euler problem 2. Having solved it I started to look around to see how else it could be done. The ruby doc for the [Enumerator class](http://www.ruby-doc.org/core-1.9.3/Enumerator.html) gives this more elegant example:

{% highlight ruby %}
fib = Enumerator.new do |yielder|
  a = 0
  b = 1
  loop do
    yielder << a
    a, b = b, a + b
  end
end

p fib.take(10) # => [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]
{% endhighlight %}

I've modified it slightly because I think the series should begin with 0 rather than 1. 

I then started to think about how you could test if a given number was a member of the Fibonacci sequence. Mathematically the easiest test is that that N is a Fibonacci number if and only if 

<div class="maths">
5 N<sup>2</sup> + 4 or 5N<sup>2</sup> – 4 is a perfect square.
</div>

i.e. if either of those terms is the square of an integer. This led me to this simple monkey patch method for the Numeric class:

{% highlight ruby %}
class Numeric
  
  def fibonacci?
    if (Math::sqrt((5 * self**2) + 4) % 1 == 0) 
        or 
        (Math::sqrt((5 * self**2) - 4) % 1 == 0)
      return true 
    else 
      return false
    end
  end
  
end

p 8.fibonacci?
{% endhighlight %}

The modular division by 1 looks a bit horrible but a test using the .integer? method doesn’t work because sqrt always returns a float, i.e. 17.0.