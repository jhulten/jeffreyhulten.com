---
categories:
- sysadmin
- cisco
date: 2007-05-10T00:00:00Z
title: Adventures with the Cisco 871W (Part 1)
url: /2007/05/10/adventures-with-the-cisco-871w-part-1/
wordpress_id: 56
wordpress_url: http://tragicallyleet.com/2007/05/10/adventures-with-the-cisco-871w-part-1/
---

I just bought a Cisco 871W Integrated Services Router for home.  This is an attempt to add to my mad skillz by adding IOS and having a little fun learning in the process.

The box arrived today.  Inside were the router, a power supply, serial and ethernet cable, manuals, and antenna for the back of the unit.

I plugged the 871 into the wall and used the serial cable to attach it to my laptop.  Boot up hyperterminal and set the serial settings to 9600 baud, 8 bit, no parity, 1 stop bit and no flow control.  The router shows a splash screen telling you to log in with the username *cisco* and the password *cisco*.  Since factory passwords are bad, that is the first thing I wanted to change.

I logged in with the credentials provided and then floundered about for a bit trying to remember my ancient IOS skills.

First I needed to get the machine into configuration mode.  Since the account (cisco) that I logged in with was already at privilege level 15 I did not need to enable privileged EXEC mode.

    yourname# configure terminal
    yourname(config)#

There we go!  Now I was in configuration mode.  Now I needed to add my new administrative user and password to the config.

    yourname(config)# username admuser privilege 15 secret 0 secretpasswd
    yourname(config)#

Now I could log out of the cisco account and into the admuser account.

    yourname(config)# exit
    yourname# exit
    Press RETURN to get started.
    User Access Verification
    Username: admuser
    Password:
    yourname#

We have access as the admuser account, however the cisco account still exists.   Need to fix that...

    yourname# configure terminal
    yourname(config)# no username cisco
    yourname(config)#

Much better.  Now, as you may know, when you have made a change to a Cisco IOS config, you are editing the running configuration.  This means that we need to save the running configuration.  Prompt more floundering on my part until I realize that you cannot save the configuration in config mode.

    yourname(config)# exit
    yourname# copy running-config startup-config
    Destination filename [startup-config]? ENTER
    Building configuration...
    [OK]
    yourname#

Woohoo!  Got my first configuration change saved in the startup configuration.  Now for some more floundering before my next post.
