--- 
wordpress_id: 247
layout: post
title: Stupid BASH tricks...
wordpress_url: http://tragicallyleet.com/?p=247
categories:
- bash
---
From my coworker, Hiram...

{% highlight bash %}
#
# search file1 for lines not present in file2
#
cat file1 | while read i ; do if ! grep -q $i file2 ; then echo $i ; fi ; done
{% endhighlight %}

Got any BASH one liners to share?
