--- 
wordpress_id: 340
layout: post
title: NFJS - Fall 2009 - Day Two
wordpress_url: http://tragicallyleet.com/?p=340
categories:
- grails
- groovy
- nfjs
- patterns
- metaprogramming
- java
---
### Dim Sum Grails - Scott Davis

Grails is an open-source web framework written in Groovy. Grails is being used by major players like Wired.com, Taco Bell in Canada, and more. 

If you have ever created a domain (model) object in Grails and noticed the scaffolding lists fields in alphabetical order, there is a simple way past this. When you add your fields to the static constraints closure, Grails will output them in the order provided.

{% highlight groovy %}
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
{% endhighlight %}

Want to add Lucene to your application? Try this.

{% highlight text %}
> grails install-plugin searchable
{% endhighlight %}

All that is left to give yourself a search engine is add searchable=true to your domain classes.

{% highlight groovy %}
class MyObject {
	...
	static searchable = true	
	...
}
{% endhighlight %}

Once you have done that, start your application with grails run-app annd go to http://localhost:8080/app/searchable to see your search page.

### Design Patterns in Java and Groovy - Venkat Subramaniam

I have always had an interest in patterns since I attended Pattern Languages of Programming (PLoP) in 2006. Venkat refered to Java as a post-pattern language; the Gang of Four Design Patterns book came out just before Java, and so patterns are far easier to implement in Java than C++. Likewise we have power and flexibility in Groovy that we do not have in Java that enables pattern implementation.

I found myself in an interesting conversation with Barbee Davis and Ted Neward, so I was late to the next session.

### MOPping up Groovy - Venkat Subramaniam

This session was about meta-programming techniques in Groovy. My favorite part was the end where Venkat wrote a  executable DSL (domain specific language) in Groovy.

At this point I was pretty tired and none of the last set of panels really interested me, so I went home a little early.
