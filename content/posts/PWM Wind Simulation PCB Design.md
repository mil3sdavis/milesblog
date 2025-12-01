---
title: PWM Wind Simulation PCB Design
date: 2025-12-01
draft: true
tags:
  - blog
  - simracing
  - hardware
---
 # Problem

I wanted to add Wind simulation to my Sim Racing setup. As you speed up/down you get more/less wind in your face, and you get directional wind in the corners. This helps with immersion by giving a sense of speed. The PC connects to the Arduino which provides the PWM control for the fans, and the fans are then powered by an external 12v power supply.

Software and hardware designs already exist for this, but they require that you build your own interface using an Arduino. 
[SimHub](https://www.simhubdash.com/) is the software that most people use to integrate Arduino microcontrollers with sim racing software titles. SimHub allows you to choose and configure the type of Arduino you would like to use and automatically generates the Arduino Sketch file to interface with the hardware setup. The following image shows the Arduino design for a 2 fan setup using an [Arduino ProMicro](https://www.amazon.com/ATmega32U4-Micro-USB-Development-Compatible-ATmega328/dp/B07PHK8SMR). 

!![Image Description](/images/Pasted%20image%2020251201110508.png)
I implemented this design on some protoboard and got a working protype. The fans used are 12V PC case fans and require their own power supply. In this design, the +12V and GND pins of the fans are connected to an external 12V power supply and the sense pins on the fan are left unconnected, and the PWM pin is connected to the corresponding output on the Arduino. 



!![Image Description](/images/Pasted%20image%2020251201110047.jpg)

The Prototype worked very well, but was not what I would consider pretty. So I took this as an opportunity to learn how to use some PCB design software. For this project I used [EasyEDA](https://easyeda.com/)to design the PCB and [PCBWay](https://www.pcbway.com/)to manufacture the boards. The image below is the schematic design of the board. 

!![Image Description](/images/Pasted%20image%2020251201113215.png)

This is the actual board layout with routing complete. 

!![Image Description](/images/Pasted%20image%2020251201113244.png)

After routing was complete, I exported the Gerber files for the design and submitted them to PCBWay for manufacture. 

!![Image Description](/images/Pasted%20image%2020251201110056.jpg)

In a future post, I will populate the board and test it. 