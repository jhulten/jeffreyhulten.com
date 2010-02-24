--- 
wordpress_id: 304
layout: post
title: NFJS Spring 2009 - Day Three
wordpress_url: http://tragicallyleet.com/?p=304
---
<p>NOTE: I delayed posting these entries to clean up my notes and add some useful links. </p>
<p><i>GRUMPY NOTE: I lost a bunch of notes so this is based on my faulty memory and some slides.</i> </p>
<p>I got in a little late today after grabbing coffee and headed to <a href="http://michaelnygard.com/" target="_blank">Michael Nygard's</a> presentation "Architect for Scale". I love the smell of capacity math in the morning. </p>
<h3>Amdahl's Law</h3>[pmath]T_p=sigmaT_1+{(1-sigma)T_1/p}[/pmath] 
<h4>Speedup Ratio</h4>[pmath]S_p=T_1/1+sigma(p-1) [/pmath] 
<h3>Universal Scalability Law</h3>
<p>[pmath]C_p=p/1+sigma(p-1)+kappa p(p-1)[/pmath]
<br />where <br />
[pmath]sigma[/pmath] = contention <br />
[pmath]kappa[/pmath] = coherency </p>
<p>Michael mentioned a book, <a href="http://www.amazon.com/gp/product/3540261389?ie=UTF8&tag=mylibrary01-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=3540261389">Guerrilla Capacity Planning</a><img src="http://www.assoc-amazon.com/e/ir?t=mylibrary01-20&l=as2&o=1&a=3540261389" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" /> by Neil Gunther. It covers a lot of the mathematics of scalability and capacity planning.
</p>
<p>There are only two ways to increase scalability: decrease contention or decrease conherency. Why is "improve performance" not on the list? Increasing performance increases capacity. Scalability is the measure of how added resources impact added capacity. Increasing performance can reduce your need for scalability, but does not benefit scalability. An interesting side note was that increasing performance generally means making the serial portion ([pmath]sigma[/pmath]) a larger portion of the total time. This means that as you spend more time on performance, you actually create a situation where you will reach maximum capacity with fewer processing resources. </p>
<h3>Brewer's Conjecture</h3>You have heard the old quote &lsquo;Faster, better, cheaper&hellip; Pick two&rdquo;? Well when you are talking about systems architecture you can choose at most two of the following: 
<ul>
<li>Consistency</li>
<li>Availability</li>
<li>Partition-Tolerance</li></ul>Lets look at Michael's definitions: 
<dl>
<dt>Consistency</dt>
<dd>There exists a total ordering on all operations, and all nodes in the system agree on that ordering at every point in time.</dd>
<dt>Availability</dt>
<dd>Every request received by a non-failing node must result in a response</dd>
<dt>Partition-Tolerance</dt>
<dd>The network may lose arbitrarily many messages from any subset of nodes to any other subset of nodes.</dd></dl>
<p>You want your system to be consistent and available? Partitioning is not allowed. How are you going to prevent partitioning? Do you expect servers, switches and network cards to never fail? This is unrealistic. </p>
<p>You want your system to be consistent and partitionable? Consistency can only be guarenteed if the service is unavailble during partitions. Otherwise you end up with 'split-brain'. </p>
<p>You want your system to be available and partionable? We maintain availablity during partitions by allowing different subsets to report different histories. This means that agreement or syncronization protocols are forbidden. </p>
<p>An important note: when you use and rely on ACID compliance of a relational database, you inherently select <b>Consistency</b>. </p>
<blockquote>"If you can't split it, you can't scale it." -- Randy Shoup, eBay</blockquote>
<p>All partitioning strategies assume no cross-cluster dependencies on shared data. Shared writable data requires serialized access which raised [pmath]sigma[/pmath]. </p>

<p>The database theory example for ACID compliance of a bank transaction is flawed as soon as User A and User B are with different banks. Instead of 'always consistent' we need to think about 'eventually consistent'. </p>
<a href="http://www.amazon.com/gp/product/0978739213?ie=UTF8&tag=tragicallyl33-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=0978739213"><img border="0" src="https://images-na.ssl-images-amazon.com/images/I/41Nb-knuW-L._SL160_.jpg" align="right"></a><img src="http://www.assoc-amazon.com/e/ir?t=mylibrary01-20&l=as2&o=1&a=0978739213" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />

<p>I decided to hang around for Michael's next talk, 'The 90-Minute Startup'. He talked about Amazon EC2. I lost all my notes on this talk, but seeing the cloud in action was pretty cool. </p>
<p>After lunch we had the expert panel discussion where Ken Sipe, Ted Neward, Matthew McCullough, Brian Sam-Bodden, and Michael Nygard talked about issues like the potential future of software development regulation, the potential impact of the IBM-Sun aquisition, and parallels between software engineering and the medical, legal, and construction. </p>
<p>After the panel I attended Ken Sipe's session on Java Memory, Performance, and Garbage Collection. I learned a bunch about the theory of garbage collection on the JVM. I picked up a few nice tips. To speed up your JVM startup time set your PermSpace and MaxPermSpace to the values based on what you see while your application is running. This way the JVM is not allocating space, finding is insufficent, reallocating over and over as you start up.</p>
<p>Some useful equations from the JVM memory management talk.</p>

[pmath]E=S_n-(S_n/(R_s+2))*2[/pmath]

[pmath]S_s=(S_n-E)/2[/pmath]

<br/>where<br/>
<p>[pmath]E[/pmath] = Size of Eden </p>
<p>[pmath]S_n[/pmath] = Size of New Space </p>
<p>[pmath]R_s[/pmath] = Survivor Ratio </p>
<p>[pmath]S_s[/pmath] = Size of Survivor Space </p>
<p>jps allows you to see processes either locally or remotely. </p>
<p>jstatd exposes the process information to jps over the network. A java security policy file is needed. </p>
<p>I stuck around for Ken&rsquo;s session as my last of the day, &ldquo;Debugging the Production JVM&rdquo;. After an example of VisualVM he moved into BTrace, a new feature in Java 1.6. It allows you to instrument a running JVM and get events when methods are called, or other activities take place. </p>
<p>All in all I had a great time and learned a whole bunch. </p>
