---
layout: posts
title: User stories - expressing complex decision logic using truth tables
tags: [Business analysis]
summary: Truth tables can be a useful way to express complex decision making logic within the description of an agile user story - but use sparingly.
---

*Truth tables can be a useful way to express complex decision making logic within the description of an agile user story - but use sparingly.*

The other day a developer and I were reviewing a story which contained a lot of complicated decision logic. We were struggling to understand it all until the developer reminded me of a tool I had almost forgotten existed - the [truth table](http://en.wikipedia.org/wiki/Truth_table).

A truth table is a way of describing boolean logic - if X is true and Y is false, then Z is whatever. A familiar application is specifying the behaviour of electronic gates, for example the truth table for an [AND gate](http://en.wikipedia.org/wiki/And_gate) looks like this:

<table>
<tr><th>Input 1</th><th>Input 2</th><th>Output</th></tr>
<tr><td>0</td><td>0</td><td>0</td></tr>
<tr><td>0</td><td>1</td><td>0</td></tr>
<tr><td>1</td><td>0</td><td>0</td></tr>
<tr><td>1</td><td>1</td><td>1</td></tr>
</table>

In this case the table captures what happens to the output of the circuit based on the state of two inputs - they both need to be switched on for the output to be switched on.

So how is that useful in a user story? Imagine you’ve got a story for which the acceptance criteria look like this:


**Given** *that I am not logged in*<br/>
**And** *my IP is not recognised as belonging to a customer*<br/>
**When** *I look at the welcome message on the homepage*<br/>
**Then** *It should say "Welcome, Guest"*

**Given** *that I am not logged in*<br/>
**And** *my IP is recognised as belonging to a customer*<br/>
**When** *I look at the welcome message on the homepage*<br/>
**Then** *It should say "Welcome - (Name of Company)"*<br/>

**Given** *that I am logged in*<br/>
**And** *my IP is not recognised as belonging to a customer*<br/>
**When** *I look at the welcome message on the homepage*<br/>
**Then** *It should say "Welcome, (My Name)"* 

**Given** *that I am logged in*<br/>
**And** *my IP is recognised as belonging to a customer*<br/>
**When** *I look at the welcome message on the homepage*<br/>
**Then** *It should say "Welcome, (My Name) - (Name of Company)"*


You could also describe that as follows:

<table>
<tr><th>Logged in?</th><th>Recognised customer IP?</th><th>Show</th></tr>
<tr><td>0</td><td>0</td><td> "Welcome, Guest"</td></tr>
<tr><td>0</td><td>1</td><td> "Welcome - (Name of Company)"</td></tr>
<tr><td>1</td><td>0</td><td> "Welcome, (My Name)"</td></tr>
<tr><td>1</td><td>1</td><td> "Welcome, (My Name) - (Name of Company)"</td></tr>
</table>

You’re probably thinking that for this facile example that table is complete overkill, and you’d be right. But supposing you have to take account of a third yes/no variable before deciding what to show, for example whether or not you have access to premium content. You’ve now got 8 different [permutations](http://www.mathsisfun.com/combinatorics/combinations-permutations.html) to capture:

<table>
<tr><th>Logged in?</th><th>Recognised customer IP?</th><th>Premium access?</th><th>Show</th></tr>
<tr><td>0</td><td>0</td><td>0</td><td /></tr>
<tr><td>0</td><td>0</td><td>1</td><td /></tr>
<tr><td>0</td><td>1</td><td>0</td><td /></tr>
<tr><td>0</td><td>1</td><td>1</td><td /></tr>
<tr><td>1</td><td>0</td><td>0</td><td /></tr>
<tr><td>1</td><td>0</td><td>1</td><td /></tr>
<tr><td>1</td><td>1</td><td>0</td><td /></tr>
<tr><td>1</td><td>1</td><td>1</td><td /></tr>
</table>

See how that works? The order of the table is crucial, it counts up in binary. The first row says 0 (000), the next 1 (001), then 2 (010), then 3 (011), then 4 (100), 5 (101), 6 (110) and finally 7 (111). That means all your eight combinations are present, you can’t simply forget one, as you might well do in trying to write out the acceptance criteria verbally. In fact that is exactly what was happening with the story the dev and I were working on before we switched to this method.

Now you should still write out the verbal acceptance criteria, something like this is absolutely not a substitute. It also wouldn’t work if the decision points were not binary (e.g the behaviour changed based on what country you are in). But in this case it’s a helpful addition, both in providing a neat summary of complex behaviour and in helping you ensure you find all the different cases you need to cover.

I wouldn’t employ this technique often, but there are situations where it is useful, and I’m glad to have been reminded about it.