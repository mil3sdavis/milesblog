---
title: PCB Project part 2
date: 2025-12-04
draft: false
tags:
  - blog
  - simracing
  - hardware
---
# Populated Board

I populated the board with the Arduino board and the pin headers. Assembly was very straight forward. I added pin headers for the GND and +12V lines for testing purposes, in the future I'll either add a barrel connector or just wire the power supply directly to it. 

!![Image Description](/images/Pasted%20image%2020251204102135.png)


# The Test

I used [SimHub](https://www.simhubdash.com/) top program the Arduino via USB, connected the fans to the Right and Left fan channels and used a barrel connector that has screw terminals that was able to just slide over the GND/+12V pins. 

!![Image Description](/images/Pasted%20image%2020251204102149.png)

Here is the complete setup, fans on either side of the steering wheel are adjustable and can be pointed at the player. The fan setup performed flawlessly. 

!![Image Description](/images/Pasted%20image%2020251204102158.png)


# Next Steps

- I need to add friction fit connectors on the fan headers to ensure they don't accidently disconnect.  
- 3D Design/Print a case
- Power connector solution