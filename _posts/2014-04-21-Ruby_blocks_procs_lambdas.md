---
layout: posts
title: Ruby blocks, procs and lambdas
tags: [Ruby]
summary: 
---

A self aide-memoire:

A **block** is an encapsulated bit of code that you can define when calling a method:

{% highlight ruby%}
def calculation(a, b)
  yield(a, b)
end

puts calculation(5, 6) { |a, b| a + b } # addition
puts calculation(5, 6) { |a, b| a - b } # subtraction
{% endhighlight %}

In this case if the block is not given you'll get a LocalJumpError. To guard against this you can use block.given?

{% highlight ruby%}
def foo
  if block.given? then yield end
end
{% endhighlight %}


Unlike almost everything else in Ruby, the block isn't an object. If you want to store the block in a variable and run it later on demand you need to turn it into a **Proc** or a **lambda**.

A **Proc** is a block that has been turned into an object:

{% highlight ruby%}
addition = Proc.new {|a, b| return a + b }
puts addition.call(5, 6)
{% endhighlight %}

And so is a **lambda**:

{% highlight ruby%}
addition = lambda {|a, b| return a + b }
puts addition.call(5, 6)
{% endhighlight %}

There are two main differences between procs and lambdas. One is that return behaviour is different. If you define a lambda as part of a method is behaves like you'd expected it to - the lambda returns from itself and the method carries on:

{% highlight ruby%}
def your_opinion
  opinion = lambda { return "I think it's great" }
  opinion.call
  return "I don't care what your block thinks"
end

p your_opinion #=> "I don't care what your block thinks"
{% endhighlight %}

Wheras the proc returns from the entire scope in which it was defined, i.e. it returns out of the whole method:

{% highlight ruby%}
def my_opinion
  opinion = Proc.new { return "I think it's great" }
  opinion.call
  return "I don't care what your block thinks"
end

p my_opinion #=> "I think it's great"
{% endhighlight %}

The other important different is in 'arity' - the way the objects respond to being passed the wrong number of arguments. Proc is quite tolerant of this, whereas lambda will throw an argument error.

{% highlight ruby%}
make_array = Proc.new {|a,b| [a,b] }
make_array.call(1,2) #=> [1,2]
make_array.call(1) #=> [1,nil]
make_array.call(1,2,3) #=> [1,2,3]

make_array = lambda {|a,b| [a,b] }
make_array.call(1,2) #=> [1,2]

make_array.call(1) #=> ArgumentError: wrong number of arguments (1 for 2)
make_array.call(1,2,3) #=> ArgumentError: wrong number of arguments (3 for 2)
{% endhighlight %}

Generally speaking lambdas are more predictable than procs and are preferred unless you specifically need proc behaviour. 

If you want to implicitly pass a block to a method and then turn it into a Proc object or pass it to another method then you'll need a handle to reference the block, supplied by the **& operator**.

{% highlight ruby%}
def maths(a, b)
  yield(a, b)
end

def teach_maths(a, b, &myblock)
  puts "Let's do some maths"
  puts maths(a, b, &myblock)
end

teach_maths(2, 3) { |x, y| x * y }
#=> Let's do some maths, 6
{% endhighlight %}

The passed block referred to without the '&' is a Proc:

{% highlight ruby%}
def my_method(&myblock)
  puts myblock.class
  puts myblock.call
end

my_method { 1+2 }
#=> Proc, 3
{% endhighlight %}

To go the other way and turn an explicit callable object into an implicit block:

{% highlight ruby%}
def calculation(a, b)
  yield(a, b) # yield calls an implicit (unnamed) block
end

addition = lambda {|x, y| x + y}
puts calculation(5, 5, &addition)
{% endhighlight %}

Ruby's callable objects - blocks, procs and lambdas - are all examples of a closure, because they contain both code and the reference environment of variables etc which the code needs to run. 

{% highlight ruby%}
def affair
  partner = "wife"
  yield("book hotel room with")
end

partner = "girlfriend"
affair { |y| "#{y} my #{partner}" }

#=> "book hotel room with my girlfriend"
{% endhighlight %}