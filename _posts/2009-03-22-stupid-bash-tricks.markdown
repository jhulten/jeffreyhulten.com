--- 
wordpress_id: 247
layout: post
title: Stupid BASH tricks...
wordpress_url: http://tragicallyleet.com/?p=247
---
From my coworker, Hiram...

[sourcecode lang="bash"]
#
# search file1 for lines not present in file2
#
cat file1 | while read i ; do if ! grep -q $i file2 ; then echo $i ; fi ; done
[/sourcecode]

Got any BASH one liners to share?
