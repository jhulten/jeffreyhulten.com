---
categories:
- nfjs
- architecture
- capacityplanning
- scalability
- aws
- ec2
- java
- memorymanagement
date: 2009-04-16T00:00:00Z
title: NFJS Spring 2009 - Day Three
url: /2009/04/16/nfjs-spring-2009-day-three/
wordpress_id: 304
wordpress_url: http://tragicallyleet.com/?p=304
---

NOTE: I delayed posting these entries to clean up my notes and add some useful links.

*GRUMPY NOTE: I lost a bunch of notes so this is based on my faulty memory and some slides.*

I got in a little late today after grabbing coffee and headed to [Michael Nygard's](http://michaelnygard.com/) presentation "Architect for Scale". I love the smell of capacity math in the morning.

### Amdahl's Law

$$ T_p = \sigma T_1 + ( 1 - \sigma ) \frac{T_1}{p} $$

#### Speedup Ratio

$$ S_p = \frac{ T_1 }{ 1 + \sigma(p-1) } $$ 

### Universal Scalability Law

$$ C_p = \frac{ p }{ 1+\sigma p + \kappa p(p-1)} $$

where:
&sigma; = contention
&kappa; = coherency

Michael mentioned a book, [Guerrilla Capacity Planning](http://www.amazon.com/gp/product/3540261389?ie=UTF8&tag=mylibrary01-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=3540261389) by Neil Gunther. It covers a lot of the mathematics of scalability and capacity planning.

There are only two ways to increase scalability: decrease contention or decrease coherency. Why is "improve performance" not on the list? Increasing performance increases capacity. Scalability is the measure of how added resources impact added capacity. Increasing performance can reduce your need for scalability, but does not benefit scalability. An interesting side note was that increasing performance generally means making the serial portion ( &sigma; ) a larger portion of the total time. This means that as you spend more time on performance, you actually create a situation where you will reach maximum capacity with fewer processing resources.

### Brewer's Conjecture

You have heard the old quote "Faster, better, cheaper... Pick two"? Well when you are talking about systems architecture you can choose at most two of the following: 

- Consistency
- Availability
- Partition-Tolerance

Lets look at Michael's definitions: 

Consistency:
  There exists a total ordering on all operations, and all nodes in the system agree on that ordering at every point in time.
Availability:
  Every request received by a non-failing node must result in a response
Partition-Tolerance:
  The network may lose arbitrarily many messages from any subset of nodes to any other subset of nodes.

You want your system to be consistent and available? Partitioning is not allowed. How are you going to prevent partitioning? Do you expect servers, switches and network cards to never fail? This is unrealistic.

You want your system to be consistent and partitionable? Consistency can only be guaranteed if the service is unavailable during partitions. Otherwise you end up with 'split-brain'.

You want your system to be available and partitionable? We maintain availability during partitions by allowing different subsets to report different histories. This means that agreement or synchronization protocols are forbidden.

An important note: when you use and rely on ACID compliance of a relational database, you inherently select **Consistency**.

> "If you can't split it, you can't scale it." -- Randy Shoup, eBay

All partitioning strategies assume no cross-cluster dependencies on shared data. Shared writable data requires serialized access which raised
$$ \sigma $$
.

The database theory example for ACID compliance of a bank transaction is flawed as soon as User A and User B are with different banks. Instead of 'always consistent' we need to think about 'eventually consistent'.

[![Release It!](https://images-na.ssl-images-amazon.com/images/I/41Nb-knuW-L._SL160_.jpg){: .left}](http://www.amazon.com/gp/product/0978739213?ie=UTF8&tag=tragicallyl33-20&linkCode=as2&camp=1789&creative=390957&creativeASIN=0978739213)

I decided to hang around for Michael's next talk, 'The 90-Minute Startup'. He talked about Amazon EC2. I lost all my notes on this talk, but seeing the cloud in action was pretty cool.

After lunch we had the expert panel discussion where Ken Sipe, Ted Neward, Matthew McCullough, Brian Sam-Bodden, and Michael Nygard talked about issues like the potential future of software development regulation, the potential impact of the IBM-Sun acquisition, and parallels between software engineering and the medical, legal, and construction.

After the panel I attended Ken Sipe's session on Java Memory, Performance, and Garbage Collection. I learned a bunch about the theory of garbage collection on the JVM. I picked up a few nice tips. To speed up your JVM startup time set your PermSpace and MaxPermSpace to the values based on what you see while your application is running. This way the JVM is not allocating space, finding is insufficient, reallocating over and over as you start up.

Some useful equations from the JVM memory management talk.

$$ E = S_n - ( S_n / (R_s+2) ) * 2 $$
$$ S_s=(S_n-E)/2 $$

where

$$ E = Size of Eden $$
$$ S_n  = Size of New Space $$
$$ R_s  = Survivor Ratio $$
$$ S_s  = Size of Survivor Space $$

jps allows you to see processes either locally or remotely.

jstatd exposes the process information to jps over the network. A java security policy file is needed.

I stuck around for Ken&rsquo;s session as my last of the day, &ldquo;Debugging the Production JVM&rdquo;. After an example of VisualVM he moved into BTrace, a new feature in Java 1.6. It allows you to instrument a running JVM and get events when methods are called, or other activities take place.

All in all I had a great time and learned a whole bunch.
