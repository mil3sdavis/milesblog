---
title: Electronics Repair - Automatic Fish Feeder
date: 2026-02-05
draft: false
tags:
  - blog
  - aquarium
  - petCare
  - electronics
---

## The Problem
Yesterday morning, I had discovered that my automatic feeder on my aquarium had dumped its entire hopper in the aquarium (not a big deal, it was almost empty), and was unable to retract the hopper to the original position. I initiated a manual feed via a button on the back, and the hopper would just spin and never return to initial start position. 

I initially thought that the gear mechanism had just gotten misaligned or stuck, I disassembled the feeder and reset the gears so that everything was in the correct initial state. Upon testing I ended up with the same result. This now meant that I had to figure out how the feeder knows when to retract the hopper back to the initial state at the end of the feed cycle. 

!![Image Description](/images/Pasted%20image%2020260205104736.png)

## How it works

The motor, while spinning in one direction performs a feed cycle by pushing the hopper out of the housing, and rotating it a preprogrammed number of revolutions causing it to release food from a slot in the bottom of it. When the motor spins in the opposite direction it retracts the hopper back into the housing. 

By watching the how the feeder behaved, I could tell that whatever signal it receives to tell the motor to stop and reverse direction was not being received. The gearing mechanism that extends/retracts and rotates the hopper has a tab on it that passes through an optical sensor (Data Sheet: https://www.vishay.com/docs/83763/tcst1030.pdf). The sensor uses an infrared LED and a phototransistor, the tab on the gearing mechanism passes through the gap between the LED and the phototransistor blocking the light. This is how the device knows how many times the hopper has rotated (each rotation results in the phototransistor being blocked once ), when the preprogrammed number of revolutions has occurred (in this case, two), the device reverses the polarity of the power to the motor causing it to turn in reverse and retract the hopper.






!![Image Description](/images/Pasted%20image%2020260205104930.png)!![Image Description](/images/Pasted%20image%2020260205104852.png)!![Image Description](/images/Pasted%20image%2020260205104947.png)
## The Failure

The Optical Light Sensor had failed, I could tell just by looking at it, the legs were corroded (years of use in a moist salty environment will do that). 


## The Fix

Through the magic of owning several of these automatic feeders (at one time I had several aquariums set up in my basement), and having another on that had also failed, it was time to see if i had enough working parts to make a one that works. 

The other broken feeder has also succumbed to years of hard work in a humid salty environment. The contacts in the battery compartment had corroded. The fix here was fairly simple, I hooked the contacts to the DC barrel plug up to my bench power supply to verify that the feeder still worked and it didn't have issues beyond the battery compartment. I then de-soldered the battery leads from both control boards, and attached the battery holder from the feeder with the bad sensor to the feeder that had the bad battery holder. Reassembled everything, and fed my fish their breakfast several hours late.


I'm always an advocate for trying to fix something before replacing it. If I wouldn't have had a second broken feeder to harvest parts from, I would have attempted to source a new Optical Sensor. 

## What did we learn?


In this case, I learned how this device operates, it's not just a black box that dispenses food anymore. Opening something up and figuring out how it works is a good mental exercise in problem solving that can be applied to other fields. I didn't lean any new skills here, but I was able to exercise my brain a little and save some money. 



