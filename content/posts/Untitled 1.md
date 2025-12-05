---
title: Cisco ASA Woes
date: 2025-12-05
draft: false
tags:
  - blog
  - hardware
  - cisco
  - homelab
---
# Cisco ASA 5510

I need to brush up on my networking skills, so I thought that I would dig out the old hardware that I purchased back when I initially got my CCNA certification. I figured I'd first start with this ASA Firewall since many job listing I have been seeing for Network Engineer jobs have mentioned firewall configuration.  I purchased this ASA in probably 2017 or 2018 and it was way past end of life then (foreshadowing.....).


!![Image Description](/images/Pasted%20image%2020251205104321.png)

# Configuration

I plugged the ASA into power and connected a Cisco console cable to it, i ran the other end of the console cable through an RS232 to USB adapter and opened up PuTTY. After adjusting the serial settings I was able to easily get to the login prompt.

## Logging In

This is where I hit my first snag, I had no idea what I set the username and password to 7 or 8 years ago.... So I had to do a factory reset on the ASA which isn't incredibly difficult but not something that is super intuitive. I had to interrupt the boot sequence and get into theROM Monitor (ROMmon) mode and change the configuration register for the boot sequence telling it to ignore current config on the device. From there I was able to reboot it with no loaded config, delete the stored config and then start from scratch.

I assumed that this would be the hardest part.....

!![Image Description](/images/Pasted%20image%2020251205105607.png)


## Interface Setup

From here, I set an IP address on one of the Ethernet ports and connected a laptop to that port. I setup the laptop on the same subnet and pinged the ASA successfully. I then enabled the http server on the ASA to enable access to the web GUI.

!![Image Description](/images/Pasted%20image%2020251205105723.png)

## Disaster Strikes

I attempted to visit the web GUI in my browser, only to be greeted with an SSL/TLS mismatch error.... uh oh.  A quick web search revealed that this version of the ASA firmware only supports TLS 1.0 and the only fix is a firmware upgrade. Well that seems easy.... except Cisco doesn't just give out firmware files, and even if I still had an account with them that had access to updates, it would appear that they no longer have the files available for this ASA because it is soo old (eol was in 2018). 

I was about to give up, but remembered that I had a laptop that hasn't been booted up in almost as long as this ASA and though maybe it might work to access the web GUI. I set that laptop up, attempted to access the web GUI in Chrome and received the same error. Then I realized that this laptop still had Internet Explorer on it. I tried in IE, it allowed me to load the page after choosing to ignore the certificate errors..... At this point I thought my problems were solved.

The GUI for the ASA (Cisco ASDM) is a JAVA program, so the webpage loaded on the ASA is really just a download page for the JAVA file. I downloaded the file, but when I went to run it, the PC let me know that I didn't have JAVA installed... ok fine, so I installed Java and tried again. 

The latest version of Java doesn't support the ASDM file. So after another Google search I found many people with the same issue. The only solution appears to be to downgrade Java.... but these posts were from  8 years ago... and that version of Java is long gone.....

## Conclusion

This ASA is now basically just a giant piece of e-waste. I did a little bit of searching to see if maybe it was possible to install some sort of alternate firmware on it like OpenWRT, but it would appear that most projects like that don't support Cisco hardware because it is too specialized. So, I guess now I'm gonna need to find another firewall to play with.... looked at some Palo Alto PA-820's on eBay, they don't go eol until 2029, so that's probably a good choice.... just gonna have to wait until after the holidays. 