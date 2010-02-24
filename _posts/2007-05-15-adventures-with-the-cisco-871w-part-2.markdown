--- 
wordpress_id: 57
layout: post
title: Adventures with the Cisco 871W (Part 2)
wordpress_url: http://tragicallyleet.com/2007/05/15/adventures-with-the-cisco-871w-part-2/
---
In the [previous post](http://tragicallyleet.com/2007/05/10/adventures-with-the-cisco-871w-part-1/), I got my new Cisco 871W Integrated Services Router attached via serial cable to my laptop and changed the factory default username and password.  Next step, set the router hostname and get the new box talking on my internal network.

First step is to make sure I can recover if something goes wrong.  I found instructions on backing up my config through HyperTerminal or TFTP on [Cisco's site](http://www.cisco.com/en/US/products/sw/iosswrel/ps1835/products_tech_note09186a008020260d.shtml).

Next we set the hostname and domain.
{% highlight test %}
yourname# configure terminal
yourname(config)# hostname fw
fw(config)#
{% endhighlight %}

Notice the hostname change took effect immediately.

{% highlight test %}
fw(config)# ip domain name domain.com
fw(config)# exit
fw# copy running-config startup-config
{% endhighlight %}

Now the new hostname and domain name are saved to the startup configuration.  Next up, setting the network information.

{% highlight test %}
fw#show ip interface
FastEthernet0 is up, line protocol is down
  Internet protocol processing disabled
FastEthernet1 is up, line protocol is down
  Internet protocol processing disabled
FastEthernet2 is up, line protocol is down
  Internet protocol processing disabled
FastEthernet3 is down, line protocol is down
  Internet protocol processing disabled
FastEthernet4 is administratively down, line protocol is down
  Internet protocol processing disabled
Dot11Radio0 is administratively down, line protocol is down
  Internet protocol processing disabled
Vlan1 is up, line protocol is down
  Internet address is 10.10.10.1/29
  Broadcast address is 255.255.255.255
  -- Cut --
Virtual-Dot11Radio0 is administratively down, line protocol is down
  Internet protocol processing disabled
fw#
{% endhighlight %}

{% highlight test %}
fw#show vlans 

No Virtual LANs configured.

fw#
{% endhighlight %}

Wait a second!  "No Virtual LANs configured"?   The interfaces show Vlan1 is up?

{% highlight test %}
fw#show vlan-switch
VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0, Fa1, Fa2, Fa3
1002 fddi-default                     active
1003 token-ring-default               active
1004 fddinet-default                  active
1005 trnet-default                    active    

VLAN Type  SAID       MTU   Parent RingNo BridgeNo Stp  BrdgMode Trans1 Trans2
---- ----- ---------- ----- ------ ------ -------- ---- -------- ------ ------
1    enet  100001     1500  -      -      -        -    -        1002   1003
1002 fddi  101002     1500  -      -      -        -    -        1      1003
1003 tr    101003     1500  1005   0      -        -    srb      1      1002
1004 fdnet 101004     1500  -      -      1        ibm  -        0      0
1005 trnet 101005     1500  -      -      1        ibm  -        0      0   

fw#
{% endhighlight %}

Aha!  Vlan1 is the default Virtual LAN and all ports are assigned to it.  Since I do not have the Advanced IP Services Cisco IOS Software Image I cannot add more Virtual LANs.  With Advanced IP Services I can have up to four VLANs on the 871W.  Looks like I need to configure the default VLAN.

{% highlight test %}
fw#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
fw(config)#interface Vlan1
fw(config-if)#ip address 192.168.138.1 255.255.255.0
fw(config-if)#no ip route-cache
fw(config-if)#exit
fw(config)#exit
fw# copy running-config startup-config
fw#
{% endhighlight %}

Now all the internal interfaces on my router are configured to the 192.168.69.0/24 network.  Next up, setting up the DHCP server!
