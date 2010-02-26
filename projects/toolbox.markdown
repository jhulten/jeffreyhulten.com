---
layout: default
title: Projects - Toolbox
---
## Toolbox

Toolbox is a simple application to manage multiple versions of tools, libraries and frameworks like Grails, Scala, and Ant.

Unpack your tools into ~/tools.  Here are my tools:

    jeffh ~/tools&gt; ls -al
    total 32
    drwxr-xr-x  15 jeffh  staff   510 Oct  8 20:23 .
    drwxr-xr-x+ 73 jeffh  staff  2482 Oct  8 20:15 ..
    -rw-r--r--@  1 jeffh  staff  6148 Sep 23 22:52 .DS_Store
    drwxr-xr-x@ 14 jeffh  staff   476 Jun 27  2008 apache-ant-1.7.1
    drwx------@  9 jeffh  staff   306 Aug  6 15:18 apache-maven-2.2.1
    drwx------@ 10 jeffh  staff   340 Sep 23 22:49 clojure_1.0.0
    lrwxr-xr-x   1 jeffh  staff    31 Oct  8 20:23 grails -&gt; /Users/jeffh/tools/grails-1.1.1
    drwxr-xr-x  17 jeffh  staff   578 Nov 14  2008 grails-1.0.4
    drwxr-xr-x@ 19 jeffh  staff   646 Sep 19 16:23 grails-1.1.1
    drwxr-xr-x@ 12 jeffh  staff   408 Jul 31 18:42 groovy-1.6.4
    lrwxr-xr-x   1 jeffh  staff    18 Feb  7  2009 scala -&gt; scala-2.7.3.final/
    drwxr-xr-x@ 10 jeffh  staff   340 Feb  5  2009 scala-2.7.3.final
    drwxr-xr-x@  9 jeffh  staff   306 Sep  9 08:46 scala-2.7.6.final
    drwxr-xr-x  14 jeffh  staff   476 Sep 23 22:55 src
    drwx------@ 16 jeffh  staff   544 Sep 23 22:55 tapestry-bin-5.1.0.5

To see the available tools:

    jeffh ~/Projects/toolbox&gt; tbx -l
    ant
    maven
    groovy
    grails
    tapestry-bin

To see the available versions of Grails:

    jeffh ~/Projects/toolbox&gt; tbx -l grails
    Current version: None
    Available versions:
      1.0.4
      1.1.1


NOTE: There is a [known issue](http://bitbucket.org/jhulten/toolbox/issue/1/) with Toolbox not finding the current version. I am working on it.

To change the current version:

    jeffh ~/Projects/toolbox&gt; tbx grails 1.1.1
    grails 1.1.1 active.

Planned Features:

- Tab Completion
- PATH Environment Variable Creation
- Common /opt/tools Repository

You can find the code on [BitBucket](http://bitbucket.org/jhulten/toolbox/downloads/) or on [PyPi](http://pypi.python.org/pypi/toolbox).
