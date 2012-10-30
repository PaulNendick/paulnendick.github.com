---
published: true
layout: article
title: Zenoss Wake-on-LAN
abstract: Waking Zenoss-monitored devices using Wake-on-LAN
author_twitter: PaulNendick
author: Paul Nendick
categories:
- articles

---

[Zenoss](http://www.zenoss.com/) is a powerful monitoring system packed with bells and whistles straight out of the box. But it lacks an obvious feature that anyone with a large network will miss: [wake-on-LAN](http://en.wikipedia.org/wiki/Wake-on-LAN).

##Who is this guide for?

* You've already gone through the trouble of [installing and configuring Zenoss](http://community.zenoss.org/community/documentation).

* You've got loads of hardware on your network with Wake-on-LAN enabled

    ![WOL Bios](/assets/images/wol-bios-enable.jpg) ![WOL Mac](/assets/images/wol-mac-enable.jpg)

* There's a machine on your network that you really want powered on but isn't. It's really far away, you're feeling lazy and it's cold outside.

![WOL machine down](/assets/images/wol-machine-down.jpg) 

## What can be done?
1. Select the target machine(s) then choose 'wakeonlan' from the Commands dropdown.

![WOL machine down](/assets/images/wol-machine-wakeup.jpg) 

2. Watch in amazement as the magic packet is sent on its way.

![WOL machine down](/assets/images/wol-send-packet.jpg) 

3. Verify the machine actually started.

![WOL machine down](/assets/images/wol-wake-success.jpg) 


## Amazing. Now how do I get this 'wakeonlan' command in my Zenoss?
1. Install the `wakeonlan` command-line utility on all of your Zenoss collector hosts

![WOL install wakeonlan command](/assets/images/wol-cli-install.png) 

   * note: users of Windows, CentOS and OS X are left to deal with their poor life choices on their own

2. Add a new command to Zenoss named 'wakeon'
![WOL zenoss new command](/assets/images/wol-new-command.png) 
![WOL zenoss name command](/assets/images/wol-command-name.png) 



3. Configure this new command. Name it however you wish but you must define the command as:
    `wakeonlan ${device/getDeviceMacaddress}`
    
![WOL zenoss name command](/assets/images/wol-configure-command.png)

Hopefully this gets you up onto your feet using `wakeonlan` with Zenoss. If you need more help or have any suggestions how this document can be improved, please leave feedback using the link below.

-Paul


