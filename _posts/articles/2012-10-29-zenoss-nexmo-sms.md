---
published: true
layout: article
title: Zenoss SMS alerts using Nexmo
abstract: Raise Zenoss alerts as SMS messages sent via Nemxo
author_twitter: PaulNendick
author: Paul Nendick
categories:
- articles

---

# Who is this guide for?
* You've already gone through the trouble of [installing and configuring Zenoss](http://community.zenoss.org/community/documentation).


* You've since learned that things in your network - important things - occasionally break.

* You would like to know when things do break. You have a mobile phone that can receieve SMS messages and can't stop thinking "There must be a solution in here somewhere!" 

# What can be done?
![SMS You Want](/assets/images/sms-you-want.png) 

# Amazing. Now how can I do this for myself?
## Prerequisites
* All your monitored devices in Zenoss are well organised into Locations, Systems, Groups, Networks, and - most importantly - Classes. If not, [take some time to do this](http://www.packtpub.com/article/zenoss-core-3x-device-setup-administration) and come back to this guide later. 

* You have an account with [Nexmo](http://nexmo.com/). Nexmo "is a cloud-based SMS API that lets you send and receive high volume of messages at wholesale rates." They're also the most cost-effective solution I know of for this task. Create an account with them,  top with a bit of credit and make note of your API key and password for later.

* 15 minutes

## Get the code
Download the [zenoss-nexmo](https://github.com/baseblack/zenoss-nexmo) code from github.
There are two files of relevance:

* `nexmomessage.py` - [marcuz/libpynexmo](https://github.com/marcuz/libpynexmo), a copy of which resides in [zenoss-nexmo/3rdParty](https://github.com/baseblack/zenoss-nexmo/tree/master/3rdParty) for safe keeping 
* `zen2nexmo` - integrates the Zenoss pager function with the API from `nexmomessage.py`

## Configure
Edit the hard-coded configuration details in `nexmomessage.py` on lines 29-32:

    try:
         msg = sys.stdin.read()    
         r = "json"
         u = "API key"
         p = "password"
         f = "BaseblackHQ"
         payload = {'reqtype': r, 'password': p, 'from': f, 'to': t, 'username':u}

* change "API key" to the 8-character alphanumberic API key provided to you by Nexmo
* change "password" to the password you selected for your Nexmo account
* change "BaseblackHQ" to what you want to see in the From: field in SMS
* keep the quotation marks
* yes, you should never code passwords into config files much less code

1. Copy `nexmomessage.py` and your modified `zen2nexmo` to the `bin` directory beneath your `$ZENHOME` Zenoss installation directory, i.e. `/opt/zenoss/zenoss/bin/`.

2. In your Zenoss settings, point the "Page Command" to zen2nexmo with the command:
`$ZENHOME/bin/zen2nexmo $RECIPIENT`

     ![SMS Nexmo command](/assets/images/sms-nexmo-command.png) 

3. Edit your user settings inside of Zenoss to include your mobile telephone number

4. Again in your user settings, add a new Alerting Rule for yourself. Click on Alerting Rules in the leftmost column then choose "Add Alerting Rule..." from the cog menu above.

    ![SMS Nexmo command](/assets/images/sms-alert-configure.png) 

## Test


#TO BE CONTINUED...