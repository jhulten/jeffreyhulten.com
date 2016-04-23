---
categories:
- nfjs
- java
- annotations
- functionalprogramming
date: 2008-09-21T00:00:00Z
title: 'No Fluff Just Stuff: Fall 2008 - Day 3 - Part 2'
url: /2008/09/21/no-fluff-just-stuff-fall-2008-day-3-part-2/
wordpress_id: 125
wordpress_url: http://tragicallyleet.com/2008/09/21/no-fluff-just-stuff-fall-2008-day-3-part-2/
---

After lunch we had the 'expert panel discussion' where the speakers. One of the great quotes was "If you use Eclipse just because it is free we have a name for that... arranged marriage. You can get some things done, but there is no love."

I then went to "The Busy Developers Guide to Annotations" with [Ted Neward](http://tedneward.com) who was on the expert group that defined the annotations facility. After a thought experiment that covered how you would mark a class as Serializable in the old Java 1.1 days we moved to a live code example implementing an annotation on a person object.

The annotation example we developed was a validation annotation. The annotation sits in front of the thing that it modifies, just like the public keyword. An annotation adds no code to the method or class it modifies, just data that is accessible via reflection. Anything that you can put annotations on has the AnnotationElement interface, including classes and methods, in the reflection API. I learned that annotations have annotations including @Retention, which specifies how long the annotation should be available, either RUNTIME, SOURCE, or CLASS, and @Target which specifies where the annotation can be used, either methods, fields, classes, constructors and more.

Annotations should never be used to carry configuration information such as filenames or defaults. They cannot be changed at runtime. Annotations are compiled to an interface by the compiler.

A great observation from Ted is that while it is not acceptable to add a keyword to a twelve year old language, it is acceptable to use a existing keyword in a new and confusing context.

For my last session of the weekend I embraced my inner masochist and attended Venkat Subramaniam's talk on Functional Programming on the Java Virtual Machine. Functional programming is focused on well-behaved functions. Some of the benefits of a functional programming model is working with multi-core machines. When your functions can be passed to functions and functions do not have side effects, you can split those functions across multiple processors without data integrity issues.

An interesting point from Venkat is to initially ignore the syntax of a language and focus on the idiom. Every programming language hurts when you first learn it, but the compiler will catch the syntax errors.

His first example was from erlang, which is a pure functional language but not on the JVM.

{{< highlight erlang >}}
main(_) -> io:format("~p", [double([1,2,3,4,5])).
double(L) -> lists:map(fun(E) -> E * 2 end, L).
{{< / highlight >}}

This takes the array 1 to 5 and runs the double function, then passes it to io:format to print to the console. The double function runs lists:map to run every element of the array and executes the anonymous function to double the value of each element.

Scala is a functional programming language that runs in the JVM. You can write Java like code in Scala, but you lose the concurrence protection.

{{< highlight scala >}}
val lst = List(1,2,3,4,5)
println(lst.map(_ * 2))
{{< / highlight >}}

This is the same functionally (no pun intended) as the erlang code above.

Its official, my brain hurts.
