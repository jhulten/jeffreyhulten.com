--- 
wordpress_id: 340
layout: post
title: NFJS - Fall 2009 - Day Two
wordpress_url: http://tragicallyleet.com/?p=340
---
<h3>Dim Sum Grails - Scott Davis</h3>

Grails is an open-source web framework written in Groovy. Grails is being used by major players like Wired.com, Taco Bell in Canada, and more. 

If you have ever created a domain (model) object in Grails and noticed the scaffolding lists fields in alphabetical order, there is a simple way past this. When you add your fields to the static constraints closure, Grails will output them in the order provided.

[sourcecode lang="groovy"]
class MyObject {
	String firstName
	String lastName
	Integer age
	
	static constraints = {
		lastName()
		firstName()
		age()
	}
}
[/sourcecode]

Want to add Lucene to your application? Try this.

[sourcecode lang="text"]
> grails install-plugin searchable
[/sourcecode]

All that is left to give yourself a search engine is add searchable=true to your domain classes.

[sourcecode lang="groovy"]
class MyObject {
	...
	static searchable = true	
	...
}
[/sourcecode]

Once you have done that, start your application with grails run-app annd go to http://localhost:8080/app/searchable to see your search page.

<h3>Design Patterns in Java and Groovy - Venkat Subramaniam</h3>

I have always had an interest in patterns since I attended Pattern Languages of Programming (PLoP) in 2006. Venkat refered to Java as a post-pattern language; the Gang of Four Design Patterns book came out just before Java, and so patterns are far easier to implement in Java than C++. Likewise we have power and flexibility in Groovy that we do not have in Java that enables pattern implementation.

I found myself in an interesting conversation with Barbee Davis and Ted Neward, so I was late to the next session.

<h3>MOPping up Groovy - Venkat Subramaniam</h3>

This session was about meta-programming techniques in Groovy. My favorite part was the end where Venkat wrote a  executable DSL (domain specific language) in Groovy.

At this point I was pretty tired and none of the last set of panels really interested me, so I went home a little early.
