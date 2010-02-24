--- 
wordpress_id: 339
layout: post
title: NFJS - Fall 2009 - Day One
wordpress_url: http://tragicallyleet.com/2009/09/21/nfjs-fall-2009-day-one-2/
---
Its that time again! The No Fluff Just Stuff : Pacific Northwest Software Symposium has returned to the Redmond Marriot.

<h3>Effective Java - Venkat Subramaniam</h3>

Unlike many talks, Venkat let us chose the topics. He put up a Jeopardy style board with catagories like 'Syntax Sugar', 'Collections' and 'Objects' and let us pick. The content varied wildly, not in its quality (Venkat knows his stuff) but in just how deep into the rabbit hole it would lead you.

As an example, which is better?

[sourcecode lang='java']
string1 + string2
new StringBuffer(string1).append(string2)
[/sourcecode]

Normally you might think that the simple + would be less efficient, but thanks to syntactic sugar the opposite is true.

In Java 1.4 and above the simple + will use StringBuilder in the background. StringBuilder will preallocate space based on expectations and will not acquire and release locks like StringBuffer will.

There were a lot of code examples and we covered pitfalls and Java strangeness like the above.

<h3>Common Antipatterns - Mark Richards</h3>

We started talking about common antipatterns in life as an example.

There are some common causes of anti-patterns:
<ul>
<li>haste - aggressive deadlines and budgets drive lower standards of quality</li>
<li>apathy - general lack of concern about finding the proper solution to a problem</li>
<li>arrogance - refusal to accept solutions or practices generally known to be effective</li>
<li>ignorance - failure (intentional or non-intentional) to seek a clear understanding of the problem space</li>
<li>pride - refusal to leverage existing designs, code and frameworks; builds everything from scratch</li>
</ul>

<b>Object Orgy</b> - insufficiently encapsulated objects result in unrestricted access to their internals.

<b>Cargo Cult Programming</b> - using patters, methods and techniques without understanding why.

<b>Golden Hammer</b> - using the same tool, product or technique to solve every problem.

With the plethora of languages available on the JVM, we have all kinds of choice. For a comprehensive list of language options, see [http://www.is-research.de/info/vmlanguages/](http://www.is-research.de/info/vmlanguages/)

<b>Accidental Complexity</b> - introducing non-essential complexity into a solution.

<blockquote>
essential complexity: we have a hard problem

accidental complexity: we have made a problem hard

"developers are drawn to complexity like moths to a flame - often with the same result" - Neal Ford
</blockquote>

<b>Lava Flow</b> - obsolete technologies and forgotten extensions leave hardened globules of dead code in its wake.

<b>The Blob</b> - an all encompassing class or component that knows too much and does too much.

Use a roles and responsibility model. Figure out in just a couple of sentences what the job of a given object is.

<b>Architecture by Implication</b> - systems lacking a clear architecture definition.

Don't rely too heavily on past experience; every problem is a little different.

<h3>Groovy Testing - Scott Davis</h3>

There are some real benefits to using Groovy for testing. Groovy has the ability to get into the private guts of a Java object.

The concept of a 'private' field is a Java <em>language</em> construct, not a Java <em>platform</em> construct. This means you can get to private methods and fields.

<h3>Keynote - Venkat Subramaniam</h3>

Venkat gave the keynote after dinner; an entertaining talk about the pointy-hairness in all of us, not just bosses.

