--- 
wordpress_id: 68
layout: post
title: Databases as a Beautiful Hammer
wordpress_url: http://tragicallyleet.com/2008/02/19/databases-as-a-beautiful-hammer/
---
From [Good Math, Bad Math](http://scienceblogs.com/goodmath/2008/01/databases_are_hammers_mapreduc.php), an article about [recent criticism](http://www.databasecolumn.com/2008/01/mapreduce-a-major-step-back.html) of the [MapReduce](http://en.wikipedia.org/wiki/MapReduce) library.

To explain MapReduce:

<!--more-->
<blockquote>

Suppose you're at work, and you need to do something that's going to take a long time to run on your computer. You don't want to wait. But you don't want to go out and spend a couple of million dollars buying a supercomputer. How do you make it run faster? One way is buy a whole bunch of cheap machines, and make it run on all of them at once. Another is to notice that your office has lots of computers - pretty much every office has a computer on the desk of every employee. And at any given moment, most of those computers aren't doing much. So why not take advantage of that? When your machine isn't doing much, you let you coworkers borrow the capability you're not using; when you need to do something, you can borrow their machines. So when you need to run something big, you can easily find a pool of a dozen machines.

MapReduce is a library that lets you adopt a particular, stylized way of programming that's easy to split among a bunch of machines. The basic idea is that you divide the job into two parts: a Map, and a Reduce. Map basically takes the problem, splits it into sub-parts, and sends the sub-parts to different machines - so all the pieces run at the same time. Reduce takes the results from the sub-parts and combines them back together to get a single answer.
</blockquote>

The problem? Well it appears that Relational Database people think that MapReduce is a crock.  The author does a great job explaining their viewpoint and what they miss:

<blockquote>
When I first wanted to spend some time learning about relational databases, my then boss told me a story about database people, which I've found to be remarkably true. The story is, RDB people have found the most beautiful, wonderful, perfect hammer in the whole world. It's perfectly balanced - not too heavy, not too light, and swings just right to pound in a nail just right every time. The grip is custom-made, fitted to the shape of the owners hand, so that they can use it all day without getting any blisters. It's also beautifully decorated - encrusted with gemstones and gold filigree - but only in places that won't detract from how well it works as a hammer. It really is the greatest hammer ever. Relational database guys love their hammer. It's just such a wonderful tool! And when they make something with it, it really comes out great. In fact, they like it so much that they think it's the only tool they need. If you give them a screw, they'll just pound it in like it's a nail. And when you point out to them that dammit, it's a screw, not a nail, they'll say "I know that. But you can't expect me to use a crappy little screwdriver when I have a magnificent hammer like this!"

That's exactly what's going on here. They've got their relational databases. RDBs are absolutely brilliant things. They're amazing tools, which can be used to build amazing software. I've done a lot of work using RDBs, and without them, I wouldn't have been able to do some of the work that I'm proudest of. I don't want to cut down RDBs at all: they're truly great. But not everything is a relational database, and not everything is naturally suited towards being treated as if it were relational. The criticisms of MapReduce all come down to: "But it's not the way relational databases would do it!" - without every realizing that that's the point. RDBs don't parallelize very well: how many RDBs do you know that can efficiently split a task among 1,000 cheap computers? RDBs don't handle non-tabular data well: RDBs are notorious for doing a poor job on recursive data structures. MapReduce isn't intended to replace relational databases: it's intended to provide a lightweight way of programming things so that they can run fast by running in parallel on a lot of machines. That's all it was intended to do.
</blockquote>

[Check it out](http://scienceblogs.com/goodmath/2008/01/databases_are_hammers_mapreduc.php) for full details.
