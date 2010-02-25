--- 
wordpress_id: 339
layout: post
title: NFJS - Fall 2009 - Day One
wordpress_url: http://tragicallyleet.com/2009/09/21/nfjs-fall-2009-day-one-2/
---
Its that time again! The No Fluff Just Stuff : Pacific Northwest Software Symposium has returned to the Redmond Marriot.

### Effective Java - Venkat Subramaniam

Unlike many talks, Venkat let us chose the topics. He put up a Jeopardy style board with categories like 'Syntax Sugar', 'Collections' and 'Objects' and let us pick. The content varied wildly, not in its quality (Venkat knows his stuff) but in just how deep into the rabbit hole it would lead you.

As an example, which is better?

{% highlight java %}
string1 + string2
new StringBuffer(string1).append(string2)
{% endhighlight %}

Normally you might think that the simple + would be less efficient, but thanks to syntactic sugar the opposite is true.

In Java 1.4 and above the simple + will use StringBuilder in the background. StringBuilder will preallocate space based on expectations and will not acquire and release locks like StringBuffer will.

There were a lot of code examples and we covered pitfalls and Java strangeness like the above.

### Common Antipatterns - Mark Richards

We started talking about common antipatterns in life as an example.

There are some common causes of anti-patterns:

- haste - aggressive deadlines and budgets drive lower standards of quality
- apathy - general lack of concern about finding the proper solution to a problem
- arrogance - refusal to accept solutions or practices generally known to be effective
- ignorance - failure (intentional or non-intentional) to seek a clear understanding of the problem space
- pride - refusal to leverage existing designs, code and frameworks; builds everything from scratch

**Object Orgy** - insufficiently encapsulated objects result in unrestricted access to their internals.

**Cargo Cult Programming** - using patters, methods and techniques without understanding why.

**Golden Hammer** - using the same tool, product or technique to solve every problem.

With the plethora of languages available on the JVM, we have all kinds of choice. For a comprehensive list of language options, see [http://www.is-research.de/info/vmlanguages/](http://www.is-research.de/info/vmlanguages/)

**Accidental Complexity** - introducing non-essential complexity into a solution.

> essential complexity: we have a hard problem
> 
> accidental complexity: we have made a problem hard
> 
> "developers are drawn to complexity like moths to a flame - often with the same result" - Neal Ford

**Lava Flow** - obsolete technologies and forgotten extensions leave hardened globules of dead code in its wake.

**The Blob** - an all encompassing class or component that knows too much and does too much.

Use a roles and responsibility model. Figure out in just a couple of sentences what the job of a given object is.

**Architecture by Implication** - systems lacking a clear architecture definition.

Don't rely too heavily on past experience; every problem is a little different.

### Groovy Testing - Scott Davis

There are some real benefits to using Groovy for testing. Groovy has the ability to get into the private guts of a Java object.

The concept of a 'private' field is a Java *language* construct, not a Java *platform* construct. This means you can get to private methods and fields.

### Keynote - Venkat Subramaniam

Venkat gave the keynote after dinner; an entertaining talk about the pointy-hairness in all of us, not just bosses.

