---
title: Electronics
author: Larry Ciscon
date: 2024-09-01
category: Design
layout: post
---

It is critical for the power from the panels to be transferred to the car with minimum losses.  There are several factors affecting this including losses occuring at each conversion stage (e.g. DC to AC), variable solar irradiance (e.g. due cloud cover), and optimizing the load the solar panels see to maximize power output. 

The solar panels put out DC voltage within a specific range.  Our 600W tower puts out 96V and the 1.2kW tower puts out 192V **if you connect all of the cells in series**.  If necessary we can lower the output voltage by connecting segments in parallel at the cost of higher current (and thus larger wires).

The most efficient solution is to feed the DC directly into the car.  This is possible if we boost the voltage to 400V and treat it like a DC fast charge station. This is possible since the NACS standard allows for power input down to a few kilowatts.  Doing it this way we should be able to achieve efficiencies in the 97% range.  We explored this option for awhile, but finally determined the unknowns and associated complexities of working with the high voltages were not worth it for now.

The solution we settled upon for the first iteration is to use a high efficiency custom microinverter design coupled with a Level 2 EV charger. 

![Martian Rover](/MartianRoadtrip/assets/images/ControllerDiagram.png)

The microinverter design we chose has a 97% efficiency. Each tower will have its own microinverter.  The AC outputs will be combined together and fed into the Level 2 EV charger and then fed into the car.  Ultimately the microinverters will be built **directly into the tower.** 

Since we will not have any additional batteries or capacitors to buffer the power output from the panels we will need to constantly monitor each stage of the process and dynamically control the charge rage to the car.  **That requires us to tap in directly to the MPPT and DC boost logic as well as the EV communications protocol.**  That is one key reason we are building and using electronics that we can customize at the hardware and firmware level.

Also the tower will incorporate a tracking camera and additional sensors to monitor weather conditions and with the help of an AI-augmented image processor anticipate changes in power output in advance so that it can renegotiate the charge rate **before** the power drops.  

The de-inverter built into the car converts the AC back into DC and into the batteries.  In theory the built-in AC-DC in the Tesla is about 95% efficient.  **So the combined system efficiency should be above 90%.**  That should be acceptable for what we need.


***
