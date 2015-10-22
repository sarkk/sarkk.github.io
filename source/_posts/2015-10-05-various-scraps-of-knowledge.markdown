---
layout: post
title: "Various scraps of knowledge"
date: 2015-10-05 09:26:25 -0400
comments: true
categories: 
---

Welcome to my first post (well, the first one with any substance). Being in the beginning stages of my learning, I don't really expect my early posts to add much (if anything at all) to the greater world of programming, but my hope is that at least my fellow learners here at Flatiron will be able to extract some value from here. 

For this one, I decided to share a couple of interesting tidbits that I came accross over the past week.

#**1. The Flip Flop Operator**

A lot of people don't seem to like this one due to its "Perlness" and apparent lack of obvious practical application, but I thought it was interesting nonetheless. By putting a range operator (..) between two conditions in a conditional statement, it will evaluate as false until the first condition evaluates as true. It will then evaluate as true until the second condition evaluates to true. Everything afterwards will then evaluate as false until the first conditional statement is true again. Take the below example:

![alt text](../images/100515/flip_flop.png)

While iterating through the array of animals, each animal is evaluated as false until we hit "dog" from the first conditional statement. Every animal after that evaluates as true until the second conditional statement, "cat", is evaluated to be true, after which all animals afterwards will evaluate as false. 

Some people seem to have found utility in this when looking for content between markers in regexes. Again, most Rubysists seem to dislike this one, but at the very least it is probably worth being familiar wtih it in case you ever see it in someone else's code.


#**2. Rescue Me**

Try and execute the following code:

x = 1/0

![alt text](../images/100515/divide_by_zero.png)

As you may have guessed, you are going to get a divided by zero error. Try do this instead:

x = 1/0 rescue nil

![alt text](../images/100515/divide_by_zero3.png)

Rescue does exactly what it implies, it "rescues" your code from any errors and returns whatever you designate. In this example, instead of throwing an error, rescue jumps in, ignores the exception, and evaluates whatever is declared afterwards, in this case nil. A lot people highly advise against using this as any exception can and will cause the rescue operation to execute, which can make debugging issues a very painful affair (and it is not hard to see how this could cause some serious unintended consequences). Still, a neat little something to at least be aware of. 

![alt text](../images/100515/divide_by_zero2.png)

#**3. To Infinity, and Beyond**

Try entering either of the below into IRB:

1/0.0

or 

1.0/0

![alt text](../images/100515/infinity3.png)

But wait, divide by 0 didn't work before in the above example, why is it working now? As per the IEEE Standard for Floating-Point Arithmetic (IEEE 754), it works when we perform the operation with floats instead of fixnums. This allows us to create ranges to represent unbounded values. 

Infinity = 1/0.0

all_positives = 0..Infinity

all_negatives = -Infinity...0

everything = -Infinity..Infinity

![alt text](../images/100515/infinity.png)

You can then use methods like take, step, first to manipulate the size and sample of what you want to use from the range. You can also use it with several enumerable methods by chaining ["Enumerable::Lazy"](http://ruby-doc.org/core-2.0.0/Enumerator/Lazy.html "Enumerable::Lazy"), which was introduced in Ruby 2.0. "In programming language theory, lazy evaluation, or call-by-need is an evaluation strategy which delays the evaluation of an expression until its value is needed (non-strict evaluation) and which also avoids repeated evaluations." ["Lazy Evaluation - From Wikipedia"](https://en.wikipedia.org/wiki/Lazy_evaluation)


