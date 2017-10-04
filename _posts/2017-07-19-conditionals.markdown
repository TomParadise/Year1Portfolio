---
layout: post
title:  conditional loops
date: 2017-07-19 12:00:00
description: what are the basic conditional loops?
category: newbie
published: true
tags:
 - c++
 - entertainment software development
---
C++ offers several simple and easy ways to loop. Loops can be used to process the same logic a number of times. The most common is the for loop, followed by while and the do-while. These loops are known as conditional because they continue to loop until a specific condition is met. 

#### the for loop ####
----

Simply defined using:
1. An initial value
2. A condition to check the value against after every iteration
3. An operation to perform after every iteration

{% highlight c++ %}

for( int i=0; i<10; ++i )
{
  // Logic goes here...
}

{% endhighlight %}

*As you can see it's basic usage is simple and easy to reason.*
