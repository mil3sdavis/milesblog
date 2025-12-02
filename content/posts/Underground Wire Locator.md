---
title: Underground Wire Locator
date: 2025-12-02
draft: false
tags:
  - blog
  - tools
---


# Invisible Dog Fence

While visiting family over Thanksgiving, my dog sitter let me know that an alarm was sounding in my garage. It turns out that alarm was the controller for our invisible dog fence (this is the one we have if you are interested https://www.amazon.com/Underground-Electric-Dog-Fence-Premium/dp/B00ZRPGLOC), stating that there was  break in the wire. 

A little explanation of how invisible dog fences work, skip ahead to the next paragraph if you are already familiar with the idea... The controller sends an RF signal down the wire which basically acts like a low power transmit antenna. From the controller, you can increase the RF power on the wire which makes the boundary line "thicker", ie more distance on either side of the wire in which the dog will be shocked. The dog wears a collar that acts as a receiver for the signal, if the dog gets too close to the wire and the collar detects the signal, they will receive a shock. There are some additional features like adjustable correction levels, but that's the basic idea of how they work. 

Finding a break in a wire that is buried is not generally an easy task, but there is a tool made for this job, the Underground Wire Locator (this is one I purchased for another project that I haven't gotten around to yet  https://www.amazon.com/dp/B08NPKY94N). This works in a very similar way to how the invisible fence works. The locator puts an RF signal on the buried wire and then the user (me) wanders around with a receiver that has an antenna on a weight that hangs near the ground.  By swinging the weighted antenna back and forth like a pendulum you can hone in on the location of the wire by listening to the strength of the tone on the receiver. When the receiver antenna is directly above the buried wire the tone is very weak, but it is strong on either side of the wire. 

![[Pasted image 20251202145404.png|300]]

I am by no means an RF engineer, but I did stay at a Holiday Inn Express last week in Ohio, and I do have my Extra Class Amateur Radio License (Callsign N8MEM), so I will attempt to explain how this works. The wire in the ground is horizontally polarized while the antenna on the receiver is vertically polarized (this is due to how it is held). When the receiver is directly above the wire the antenna is not receiving the signal at all because it is at a right angle to the direction that the signal is being propagated from the wire in the ground. BUT, if you swing the receiving antenna like a pendulum, as soon as the pendulum passes dead center, the receive angle becomes less than 90 degrees and the receive angle of the antenna intersects with the transmit angle of the wire in the ground. I hope that makes sense, I'm sure there are better terms that could be used, but it gets a little out of my area of expertise. 

I was able to find the break in the wire this way, eventually I got to a point in the wire where I no longer had any signal, and I had to dig through 12 inches of snow and some leaves (luckily I live in the woods, and most of the wire was just laid on the ground and has naturally been covered over time). The break was at a splice I had put in the line when I setup the fence, somehow it had come disconnected, not sure what happened, because I didn't actually find the exact spot, I pulled the cable up out of the snow while locating it and suddenly I had the end of the wire. I then had to go back to the transmitter and put it on the other end of the wire and then trace it to where it stopped and dig around in the snow for a bit to find the other end. I twisted them back together with a wire nut and stuck them in a  plastic connector box full of some sort of dielectric grease made for this application.


# What Frequency Does this Thing Operate On?

This is now where things get interesting.... Curiosity got the best of me, and I started to wonder what frequency this tester is using for it's RF signal. So I went to the manual....

![[Pasted image 20251202153125.png|300]]


200kHz, well mystery solved....200-275kHz frequencies in the United States are allocated for Aeronautical Radio Navigation and Aeronautical Mobile Radio Use (Check out this awesome chart here... [United States Frequency Allocations ](https://www.ntia.gov/sites/default/files/2025-09/ntia-us-frequency-allocations.pdf)). 

I wasn't satisfied, I setup my [SDRPlay](https://www.sdrplay.com/), Tuned the software to 200kHz and noticed something very interesting when I turned on the transmitter. 

![[Pasted image 20251202153819.png|300]]

It is actually transmitting on 455kHz. Which is a frequency allocated for Maritime Mobile radio use and Aeronautical Radio Navigation.  

!![Image Description](/images/455khz%201.jpg)

I haven't done much research in to the manufacturer besides trying to visit their website that is on the back page of the manual, http:www.kolsol.net, which conveniently gives a "404 Not Found" error. Based off the English in the manual I'm assuming this was probably a short lived Chinese company....The seal of quality on the manual cover tells you everything you need to know.... "Original AUTHENTIC, Patented products, Counterfeiting not allowed."