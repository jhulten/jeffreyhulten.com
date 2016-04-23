---
categories:
- maven
- nfjs
- java
date: 2008-09-21T00:00:00Z
title: 'No Fluff Just Stuff: Fall 2008 - Day 3 - Part 1'
url: /2008/09/21/no-fluff-just-stuff-fall-2008-day-3-part-1/
wordpress_id: 122
wordpress_url: http://tragicallyleet.com/2008/09/21/no-fluff-just-stuff-fall-2008-day-3-part-1/
---

I got in a little late today, about 0845, which meant a fast breakfast and then off to the first session: Managing Project Integrity with David Bock of [CodeSherpas](http://codesherpas.com). This session was a whirlwind tour of tools to provide greater management and documentation of your code, from Maven to jDepend, Xradar to PMD. I didn't have power for my laptop and the battery was near dead so I don't have a lot of notes on the topic, but I do have a few ideas.

Next session was also with David Bock, Intermediate Maven. For those who do not know Maven it is a build management tools similar in some ways to Ant. I understand so much more than I did about Maven, especially the simple things like what the points in the lifecycle are and what order they run in. I am sure this is documented somewhere, but I just haven't found it.

We got into a great discussion about using private repositories to manage dependencies like Archiva or Artifactory. Between making sure that you always get the same version of, for instance, jUnit 3.8.1 and lowering your initial project setup time by caching those packages there doesn't seem to be much reason not to set one up. Just make sure you back it up!

Then we got into running Ant tasks inside of Maven, which is very cool. The ease of adding existing Ant targets to a lifecycle phase in Maven is slick. I will see about posting some examples of this later on.

Writing Maven plugins are pretty trivial. Maven gives you an archetype to build a base package and then it is just customization (maven-archetype-mojo). The process is pretty simple to build out, however it adds more complexity to your build process real fast.

Next is lunch followed by the expert panel discussion.
