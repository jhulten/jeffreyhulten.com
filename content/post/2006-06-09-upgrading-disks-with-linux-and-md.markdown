---
categories:
- sysadmin
- linux
date: 2006-06-09T00:00:00Z
title: Upgrading Disks with Linux and MD
url: /2006/06/09/upgrading-disks-with-linux-and-md/
wordpress_id: 22
wordpress_url: http://tragicallyleet.com/2006/06/09/upgrading-disks-with-linux-and-md/
---

So I have a server that was out of disk space. Since it held a database I did not want to have to rebuild it, plus I am lazy so there had to be an easier way. The drives were mirrored using the ***md*** driver under linux.  This was my chance to figure out how to rebuild a mirrored drive.<!--more-->

First things first. I did not want anything to run against this server while I was upgrading so I disabled the MySQL cluster and remote cron jobs. Then it was time to put the server in single user mode. I could try and catch it at the right time or pass specific parameters at boot time, but like I said I am lazy. I edited the /etc/inittab and searched for a line that looked like:

    id:3:initdefault:

This sets the default runlevel for the system.  One quick edit later and I have:

    id:1:initdefault:

This will load the system into single user mode when booting until I tell it different.

Next step was to shut down the box and replace the second drive. I replaced the second drive because I was pretty sure that I had not installed the boot loader on the first drive. Once the second drive was in place I booted up.

I found a nice utility for cloning the partition table.  It is called ***sfdisk***. This command will let you do all sorts of great (and if you are not careful, nasty) things to your disks. The command was simple... Since /dev/sda was my existing disk and /dev/sdb was the new one, the command was:

    sfdisk -d /dev/sda | sfdisk /dev/sdb

This cloned the partition table to the new disk. You may find that the command for /dev/sdb needs a --force flag to run. More information about sfdisk can be found at <http://www.die.net/doc/linux/man/man8/sfdisk.8.html>.

Since Linux does not always catch when you have a partition table change, I rebooted the server to allow it to sync up. Then the fun part; rebuilding the mirror.

Now you have a md device with only one member. To add your newly partitioned drive to the md device and start the mirror rebuilding, use the mdadm command. To get help on the mdadm command, use the man page or type ***mdadm --help***.

If you are rebuilding md0 from the existing device /dev/sda1 you can run:

    mdadm --manage /dev/md0 --add /dev/sdb1

This will add the new partition and start rebuilding the mirror.  To check on the status, run:

    cat /proc/mdstat

***mdstat*** contains all the information you need on the configuration of your software raid devices.

    Personalities : [raid1]
    md0 : active raid1 sda1[0] sdb1[1]
    811136 blocks [2/1] [U_]
    [====>................]  recovery = 24.8% (231450/811136) finish=0.5min speed=80754K/sec


Once it is complete you will see:

    Personalities : [raid1]
    md0 : active raid1 sda1[0] sdb1[1]
    811136 blocks [2/2] [UU]

If you have more than one partition to mirror, run the command for the other md devices. They will wait until the first one is complete.

At this point you need to install you boot loader on the new disk.  This process will vary depending on the bootloader you have chosen.

Take your old disk out and swap in the second new disk.  Repeat the process and set the init level back to 3.

Let me know if this works for you or not.  As always these instructions are my own recollection of the steps I went through and you use them at your own risk.

