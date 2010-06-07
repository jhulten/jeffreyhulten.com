---
title: Linuxfest Northwest 2010
layout: post
categories:
- lfnw
- linux
---
I decided to attend [Linuxfest Northwest](http://linuxfestnorthwest.org) in Bellingham, WA this year. This was a learning opportunity, a networking opportunity, and a chance to stay with [my sister](http://stillseekingsanity.com) for the weekend.

###Monitoring Bare Metal to the Clouds with Zenoss

[Zenoss](http://zenoss.com) is a open-source enterprise IT monitoring tool written in Python. They have far reaching coverage into both operating systems, server applications and the applications you run on them. Each device you set up goes into a single device class, which defines templates, properties, and collector plugins. Devices also are in locations which group devices geographically and allows definitions of the networks between them. Groups and systems tag your devices to provide logical grouping of your applications. 

###Drizzle with Brian Aker

I know Brian from the real world, so I looking forward to this talk as I have not seen his talk before. The world of Drizzle, a next-generation fork of MySQL, started with the 5.0 Customer Advisory Board. It was obvious to Brian that they had missed the mark with 5.0. The first step was to focus on tomorrow: focus on 64-bit, SSD drives, multi-core servers, modern application infrastructure, and using C++, STL and Boost now that the compilers are consistent (unlike back in the beginning of the MySQL days).

Extending ease of use is the next part of the vision. Treat BLOBs as blobs, don't bother with TINYBLOB or LARGEBLOB. Text fields are all stored as UTF-8. UTF-8 is the character format of the web. Eliminating gotchas as well: no bad inserts, no hidden truncations, no filesystem case sensitivity, and no modes.

Making the database infrastructure aware was next. Authentication uses PAM and LDAP instead of an internal system which allows the database to be part of a larger architecture. The point is to take the monolithic database and break it into a microkernel and a series of plugins.


