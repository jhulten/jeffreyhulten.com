---
categories:
- bash
date: 2009-03-22T00:00:00Z
title: Stupid BASH tricks...
url: /2009/03/22/stupid-bash-tricks/
wordpress_id: 247
wordpress_url: http://tragicallyleet.com/?p=247
---

From my coworker, Hiram...

{{< highlight bash >}}
#
# search file1 for lines not present in file2
#
cat file1 | while read i ; do if ! grep -q $i file2 ; then echo $i ; fi ; done
{{< / highlight >}}

Got any BASH one liners to share?
