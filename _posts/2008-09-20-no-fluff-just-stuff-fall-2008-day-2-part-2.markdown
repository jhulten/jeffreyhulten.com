--- 
wordpress_id: 117
layout: post
title: "No Fluff Just Stuff: Fall 2008 - Day 2 - Part 2"
wordpress_url: http://tragicallyleet.com/?p=117
---
After lunch I bought a few books and then headed to the 'mystery panel' (a typo on the schedule) about Code Metrics with Neal Ford. After a brief tour of tools we started to talk about the meaning of various metrics. First, KLOC or thousands of lines of code is meaningless or worse.

Cyclomatic complexity measures the complexity of a function. The basis of this is metric is pretty simple. Treating the code as a graph G where statements are nodes and paths are edges the metric is V(G) = e - n + 2 where e is the number of edges and n is the number of nodes.

FLOG is a tool for Ruby that assigns a value to each type of action, such as literals, branching, assignment, etc. Add the values of the actions and you get a sense of the complexity of the function. Neal said that you can run FLOG on the codebase of any Ruby project and the file with the highest score is almost guaranteed to be the one with the most bugs.

Next he covered the Chidamber and Kemerer object-oriented metrics. They covered two types; easy but not useful and very useful. The latter category includes the # of methods executed due to the method call, sum of other classes that this class uses, and the sum of how many classes use this class.

A side note, he was using a tool on the Mac called oXygen that provided a fairly sane way to work with XML documents.

jdepend was the next tool he covered, which reports based on packages instead of classes. It calculates the efferent and afferent couplings, just like the C&amp;K OO Metrics but extrapolates instability, abstractness, and distance from the main sequence. Distance from the main sequence states that packages should either be very abstract and highly stable, or highly unstable but very concrete.

All in all a lot of great content, especially on communicating the metrics as a part of developer motivation, etc.

My last official session of the day was titled &quot;The Busy Java Developer's Guide to Performance and Scalability&quot;. Ted Neward is a self-proclaimed language whore, with books on Java, XML, and .NET under his belt.

He had a simple definition of performance and scalability. Performance is how fast the application responds to an end user. Scalability is the number of users you can support.

His steps were pretty straightforward:

- Know your performance and scalability goals.
- Avoid the pitfalls of assumptions.
- Measure, measure, measure.
- Refactor or redesign as necessary.

The base assumptions to avoid are pretty obvious, but as developers we seem to ignore:

- Myth: bandwidth is infinite
- Myth: latency is zero
- Myth: transport cost is zero
- Myth: topology doesn't change
- Myth: the system is homogeneous
- Myth: you &quot;know&quot; where slowdowns and bottlenecks are

These are all great points to remember are NOT true. If you look at the difference between google.com and amazon.com home pages are a great example of myth one. Amazon seems to think that bandwidth is infinite, where Google understands that it is not!

One of the tools he demonstrated was jConsole, where you can view the memory, CPU and other metrics about your application.  This hits on myth six; do not assume you know where your issues are.  Measurement is the only meaningful way to evaluate your code.

Another great day, Birds of a Feather sessions next then I am off home.