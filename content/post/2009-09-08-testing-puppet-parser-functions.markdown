---
categories:
- ruby
- puppet
- testing
date: 2009-09-08T00:00:00Z
title: Testing Puppet Parser Functions
url: /2009/09/08/testing-puppet-parser-functions/
wordpress_id: 324
wordpress_url: http://tragicallyleet.com/?p=324
---

I have been working on some parser functions for Puppet. Specifically I was using the example from the [wiki](http://reductivelabs.com/trac/puppet/wiki/WritingYourOwnFunctions):

{{< highlight ruby >}}
require 'ipaddr'
module Puppet::Parser::Functions
	newfunction(:minute_from_address, :type => :rvalue) do |args|
		IPAddr.new(lookupvar('ipaddress')).to_i % 60
	end
end
{{< / highlight >}}

I wanted to test this function so I started up irb, including the puppet library and my function file...

{{< highlight bash >}}
% irb -r puppet -r time_from_facts.rb
>>
{{< / highlight >}}

To make sure that the function was loaded I used the 'function' call in the Puppet::Parser::Functions.

{{< highlight irb >}}
>> Puppet::Parser::Functions::function(:minute_from_address)
=> "function_minute_from_address"
{{< / highlight >}}

This shows that the function was loaded. We can then test the function by instanciating a parser scope object:

{{< highlight irb >}}
>> s = Puppet::Parser::Scope.new
=> #<Puppet::Parser::Scope:0x12fb984 @defaults={}, @symtable={}, @namespaces=[""], @tags=[]>
{{< / highlight >}}

Once the scope is created I can set variables that may be used in the function, specifically 'ipaddress' in this example:

{{< highlight irb >}}
>> s.setvar('ipaddress','192.168.205.12')
=> "192.168.205.12"
{{< / highlight >}}

With the variable set all that is left is to call the function and see what happens:

{{< highlight irb >}}
>> s.function_minute_from_address
=> 52
{{< / highlight >}}

Hope this helps some of you with testing your Puppet functions.
