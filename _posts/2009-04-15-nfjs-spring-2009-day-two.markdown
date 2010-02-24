--- 
wordpress_id: 303
layout: post
title: NFJS Spring 2009 - Day Two
wordpress_url: http://tragicallyleet.com/?p=303
---

<em>NOTE: I delayed posting these entries to clean up my notes and add some useful links.</em>

After getting to the hotel about ten minutes beforehand, I started the day with Ted Neward's talk, 'The Busy Developers Guide to Java Platform Security'. Instead of a "boring" presentation Ted decided it was story time.

He told the story of deciding that technology was the path to burnout and he would start his own bank, steal from it and then get bailout money. He hires a guard to stand in front of the vault and check the credentials of everyone coming in and out of the vault. He then hires a teller to be the front end of his bank.

TED hires GUARD

GUARD allows all people deposit(*) and withdraw(300)

GUARD checks permissions on BOB depositing $10<br />BOB succeeds

This is GOOD

GUARD checks permissions on CARLOS (the terrorist) withdrawing $100<br />CARLOS succeeds 

This is BAD

TED hires TELLER

TELLER has deposit(*) and withdraw(300) permission<br />GUARD only allows people with the right permissions to access the vault

GUARD checks permissions of TELLER (succeed) and then the object that TELLER is acting on behalf of (CARLOS)<br />CARLOS attempts to withdrawl $100, which he does not have permissions to do<br />GUARD kills CARLOS with PINKYOFDEATH 

This is GOOD

GUARD checks permissions of TELLER (succeed) and then the object that TELLER is acting on behalf of (BOB)<br />Bob attempts to deposit $10, which he does not have permission to do<br />GUARD kills BOB with PINKYOFDEATH

This is BAD

TED tells TELLER to show a priveledge flag if it doing something on behalf of another

TELLER starts checking if someone can deposit or withdraw a given amount, shows a priveledge activity flag (business logic)

In this simplified version of Ted's roleplaying, the following 'characters' represented the following parts of a Java-based application:
<ul>
<li>TED = Developer </li>
<li>GUARD = Access Controller, checks permissions to an access domain </li>
<li>TELLER = Run Time Library (rt.jar) and business logic</li>
<li>PINKYOFDEATH = AccessControlException </li></ul>

To turn on the security manager you add the -Djava.security.manager flag to the java command line. It references the jre/lib/security/java.policy file for the JRE. 

{% highlight %} 
grant [codeBase PATH|signedBy KEY] { 
permission PermissionClass ACTION 
} 
{% endhighlight %} 

### IMPORTANT SAFETY TIP!

To UNION the JRE security policy with your security policy, include -Djava.security.policy=your.policy in how you run the java executable. To REPLACE the JRE standard policy with your security policy, use two equals signs (-Djava.security.policy==your.policy). If the action fails for the target it throws an AccessControlException.

I was impressed by Ted's talk and decided to stick around for his Busy Java Developers Guide to Advanced Platform Security. The key topics he covered were:

<ul>
<li>security debugging</li> 
<li>custom Permissions </li>
<li>jar signing for server permissions</li> 
<li>custom Access Controller contexts </li>
</ul>

Security debugging can be activated with -Djava.security.debug=FLAG where FLAG is one of all, jar, policy, scl, or access. The jar flag is for testing JAR signing. The policy flag is good to make sure your policy file is being read and parsed correctly. If a policy file has a syntatical error in is (missing semicolon, etc.), if a policy has a malformed URL. The permissions attempt to be instanciated by the security manager but the classpath is not established so it marks the permission class as unresolved and expects it to be provided at runtime. If the permission policy does not exist, the permission is not granted but the policy as a whole is still in play. The scl flag dumps information when ClassLoader assigns permissions to classes. It isn't as useful as policy and access. The access flag on java.security.debug will print all checkPermission results. The three suboptions are stack, domain, and failure which show a stacktrace during the checkPermission call, the protection domain during the call, and additional information during a failure respectively. java -Djava.security.manager -Djava.security.debug=access:stack,domain,failure AppClass 

{% highlight java %} 
public class Util { 
	public static void doSomething() { 
		AccessController.checkPermission(new RuntimePermission("insult")); 
		System.out.println("You're ugly!"); 
	} 
} 
{% endhighlight %}

This checks the RuntimePermission regardless if the security manager is enabled or not. The AccessController class exists NO MATTER WHAT. 

{% highlight java %} 
public class Util { 
	public static void doSomething() { 
		if (System.getSecurityManager() != null) AccessController.checkPermission(new RuntimePermission("insult")); 
		System.out.println("You're ugly!"); 
	} 
} 
{% endhighlight %}

Now only if the security manager is enabled, the check is called. He then covered writing custom permission classes which is where my typing fell behind. It is pretty simple stuff though. The key seemed to be the implementation of the 'implies' method on your permission class. Finally he covered signing jars, which is not particularly useful unless you also include the key in the security policy and get your key signed by a third party such as Verisign. 

While my brain did not feel as full as last time, my stomach was empty and I was glad for the lunch break. Buttermilk fried chicken, mashed potatoes and apple pie made for a nice midday meal. 

After lunch one of my coworkers (and one of my groomsmen from my wedding last year) and I went to the "Beginning Drools: Rules Engines in Java" presented by [Brian Sam-Bodden](http://www.nofluffjuststuff.com/conference/speaker/brian_sam-bodden.html). 

The real joy of a rule engine is that you can move to fact-based evaluation of code instead of massive nested IF/THEN structures. 

Rules need to be discrete encapsilation of knowledge. For instance, "if it is sunny outside, you need sunscreen". The firing of a rule can result in the modification, addition or removal of existing facts. Facts are purely assertions about the problem. For instance: 

{% highlight %} 
when: there are two people and they share a only one parent 
then: they are half-siblings 
{% endhighlight %}

A rule engine is a system that matches facts and data against production rules. It derives or infers conclusions from premisies by using rules. 

The inference engine is the component of the rule engines that matches facts against the production rules. They use pattern matching algorithms such as linear, rete, treat, or leaps. Drools uses the rete algorithm. 

Chaining is reasoning using inference rules. The two main methods are forward chaining and backwards chaining. Forward chaining starts with a base set of facts and infers more facts until a desired goal is reached. This type of recursive processing requires a stop condition to let the engine know when to stop processing. Drools does support a timeout that allows you to determine how long you should be allowed to process the request. 

Forward chaining is data-driven. Backwards chaining is goal driven. It starts with a list of goals you want to achieve and infers the data that will satisfy the goals by working backwards. 

Consequence of a rule should never include the execution of tasks outside of adding, changing or removing facts. Do not implement the things you want to do based on the facts in the consequences, that belongs in other components. 

Since the Rete algorithm is the 'secret sauce' of many rule engines it is good to understand at a high level how it works. The rule engine is composed of the inference engine, the rule base, and working memory which contains all the facts. The rule base in the full set of production rules, which is them read into the inference engine as a Rete network. A Rete network is a tree of nodes, where every node is the predicate of a rule and the consequence of the rule is added to the facts as the input of the next node. Inside the inference engine, rules are matched againsts facts in the working memory using the pattern matcher (Rete). The unordered list of 'activations' or matched rules is ordered into the agenda which is the conflict resolver. The first rule of the agenda is fired, which may trigger the process all over again. Drools in particular is a forward chaining inference engine based on the Rete algorithm. 

You define your rules either in XML (blech) or the Drools Rule Language that is parsed into AST and then into a package. That package is applied to the working memory, which includes the truth maintenance system, the agenda with agenda event support, and working memory event support. Here is an overly simple example of the Drools Rule Language: 

{% highlight %} 
rule "MyRuleName" 
	when predicate 
	then consequence 
end 
{% endhighlight %}

In the predicate you match at the class level, so you have to be careful about including primatives like Integer because if you include two integers it will not know which one it is supposed to work with. 

I decided to stick around for the Advanced Rules Programming with Drools presentation with Brian Sam-Bodden. To do a proper Advanced class he would need a couple of days, so he said we would probably be at about an intermediate level. 

The Drools IDE for Eclipse 3.2 or higher is highly recommended. You will be able to create a new rule project and other project artifacts. As a side note he talked about a nice feature that allows you to use Excel spreadsheets as decision tables for rule generation. This is great if you are in an environment where business analysts are generating rules. 

Domain Specific Languages in Drools allows you to extend the rule language to your problem domain, which enables programmers to get away from business policy and focusing on implementation. It simplifies the rule base by removing domain specific duplication and has no performance impact at runtime. The DSL specification specifies natural language on the left and the DRL syntax on the right. 

{% highlight %} 
[condition]If there is a Person with the age of "{name}"=Person(name=="{name}") 
[consequence]Say {message}=System.out.println("{message}"); 
{% endhighlight %}

You can also add a duration operator that will wait to fire a rule after the conditions are true until the time (in milliseconds) elapse. He covered alot of great examples of DSL rule implementation in Drools, but I am not even going to try to capture them here. 

We then moved into grouping rules and controlling flow. After a brief review of salience, agenda groups and agenda filters he moved to his preferred method: rule flows. I did not entirely understand his description, but there is definitely alot of power there. Drools is powerful by itself, but the addition of rule flows puts it over the top into serious mojo. This was a great session. I skipped the birds of a feather sessions so I could have a little Saturday left.
