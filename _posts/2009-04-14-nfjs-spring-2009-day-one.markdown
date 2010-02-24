--- 
wordpress_id: 294
layout: post
title: NFJS Spring 2009 - Day One
wordpress_url: http://tragicallyleet.com/?p=294
---
<em>NOTE: I am posting these entries a week and a half after the Spring 2009 event in Seattle due to time constraints in editing and such.</em>

It's my first time as an Alumni at a <a href="http://nofluffjuststuff.com">No Fluff Just Stuff</a> conference. Attendance is smaller than the Fall '08 show, but I understand that is pretty typical. I am glad to see that this conference is surviving in the lean times.

After the introduction I attended <a href="http://nealford.com">Neal Ford's</a> presentation on <a href="http://nealford.com/downloads/conferences/canonical/Neal_Ford-Emergent_Design_and_Evolutionary_Architecture-slides.pdf">Emergent Design and Evolutionary Architecture</a>. Neal's presentation is based around a series of articles he is working on for the <a href="http://www.ibm.com/developerworks/java/library/j-eaed1/">IBM DeveloperWorks</a> web site. One of the key points he made was that emerging design is really about identifying patterns (not to be confused with Patterns, such as from the GOF book, <a href="http://www.amazon.com/gp/product/0201633612?ie=UTF8&tag=tragicallyl33-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=0201633612">Design Patterns: Elements of Reusable Object-Oriented Software</a><img src="http://www.assoc-amazon.com/e/ir?t=tragicallyl33-20&l=as2&o=1&a=0201633612" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />).

<blockquote>"Software is more about communication than technology" -- Neal Ford</blockquote>

Expressiveness matters! You will probably not see patterns and potential abstractions in Assembler code. The more expressive the language (Python, Ruby and Groovy being great examples) the more likely you are to see the places where you can refactor.

A word of warning! Do not try abstracting too early in the development process. Abstractions should come from working source code, not from your preconceived ideas of what abstractions are needed.

Neal then covered one of my favorite topics, technical debt. Every project has external forces that cause compromise. The key is to convince someone in power (management) that technical debt exists and then start a conversation about repayment.

Demonstration trumps discussion in this case. Use metrics from your project like cyclomatic complexity per line of code. As a process and operations guy I am a huge fan of proper metrics. The more technical debt you have the harder it is to see the emergent design of the project.

In the end, software and application design is about code; all other artifacts are transient and should be tossed when it diverges from the code. Out-of-date documentation is worse than none because it is actively misleading. Depending on the project you may find that keeping your documentation up to date is important, but you need to take the cost into account.

Some references include Neal's <a href="http://www.amazon.com/gp/product/0596519788?ie=UTF8&tag=tragicallyl33-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=0596519788">The Productive Programmer</a><img src="http://www.assoc-amazon.com/e/ir?t=tragicallyl33-20&l=as2&o=1&a=0596519788" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" /> and <a href="http://www.amazon.com/gp/product/0596519788?ie=UTF8&tag=tragicallyl33-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=0596519788">The Productive Programmer</a><img src="http://www.assoc-amazon.com/e/ir?t=tragicallyl33-20&l=as2&o=1&a=0596519788" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />.

<!-- NOTE - XRAY FOR ECLIPSE -->After a short break we reassembled for another Neal Ford presentation, '<a href="http://nealford.com/downloads/conferences/canonical/Neal_Ford-Real_World_Refactoring-slides.pdf">Real World Refactoring</a>'. Since all the major tools provide refactoring facilities Neal focused on when and why to refactor.

First he talked about the building blocks of refactoring. ‘Composed method’ was the first, specifically divide your code into many small methods that each complete one and only one task. If you have a method longer than ten lines you have a candidate for method composition.

Once you have broken your methods up you can see if there are common pieces you can refactor up to a parent class. The key is that in the end a class can be only about one thing, shorter methods are easier to test, and you can find reusable assets where you didn't know they were there.

The second building block was SLAP or the Single Layer of Abstraction Principle. The key of this idea is that crossing layers of abstraction, like from business logic to database logic, within one method is difficult to visualize and probably a good candidate for refactoring.

<blockquote>"Refactoring is a disciplined technique for restructuring an existing body of code, altering its internal structure without changing its external behavior." -- Martin Fowler</blockquote>

Moving on he talked about decomposition, specifically taking large classes and breaking them down and decoupling from vendor libraries. It was a little complicated to try and explain which probably means I still don't understand it entirely. He did state that you should not decompose large things just because you can, they may not be evil. For example, the object representing your most important and strategic concept will probably be large and you may break the conversation with your business owners.

So you want to refactor, one of the questions people ask is if you should branch when you refactor. The real problem is the merge hell you go through at the end. To mitigate that risk, time box your efforts and don't be afraid to toss your efforts. You miscalculated the effort required and the breakage from weeks of merge hell and broken code are not worth it. Take a step back and rescope your efforts to something smaller.

One of a important refactoring issues for me is refactoring the database schema. For this there is a project called dbDeploy to help you manage the changes to your schema. One of the keys for refactoring is using triggers to synchronize data (such as in the case of moving a column) for the duration of the change window.

<a href="http://www.amazon.com/gp/product/193435614X?ie=UTF8&amp;tag=tragicallyl33-20&amp;linkCode=as2&amp;camp=1789&amp;creative=390957&amp;creativeASIN=193435614X"><img src="https://images-na.ssl-images-amazon.com/images/I/51%2BDJ2%2BWuAL._SL160_.jpg" border="0" alt="" align="right"/></a><img style="border:none !important; margin:0px !important;" src="http://www.assoc-amazon.com/e/ir?t=tragicallyl33-20&amp;l=as2&amp;o=1&amp;a=193435614X" border="0" alt="" width="1" height="1" />
Pragmatic Programmers came out with a book called 'A ThoughtWorks Anthology' which has an essay called 'Refactoring Ant Build Files'. It shows how you can apply common refactoring principals to Ant build files to remove the cruft that builds up over time.

After another break I moved over to another room to attend Scott Davis' presentation on DSLs (Domain Specific Languages) in Groovy. An example of a domain is Facebook, which we would consider a part of the social networking domain. Amazon is part of the Internet sales and cloud computing domains.

One of the dangers is attempting to put too much domain and losing the specific nature of the DSL. The joy of DSLs is the ability to build the language tools specific for the job. SQL is an example of a domain specific language as is ANT. SQL provides a strong language for retrieving data. ANT is intended just for building Java code.
