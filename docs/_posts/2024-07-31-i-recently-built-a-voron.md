---
layout: post
title:  I recently built a Voron 2.4r2
date:   2024-07-31 00:14:00 +0800
categories: [3D Printing]
comments: true
---
I was looking for a larger format 3D printer and decided to bite the bullet on getting a voron on the basis that it is a lot more moddable (vs a bambulab X1 for example). The key though is that it does not come assembled so you would have to do everything from scratch, and boy was it a journey to build given the limited time and often times frustrations with broken pieces and generally things that are not well documented as I have bought a kit that did not necessarily use all original parts. I also had to order 3D printed parts since I did not really have an enclosed printer to print ABS parts, and honestly ABS really stinks up the room quite badly

I ordered the FYSETC Voron 2.4r2 Pro CNC kit, which in general was a great kit if you knew how to put it together. The initial challenge I had was due to the CNC kit, which was different from the documented 3D printed parts. I eventually found the video on youtube after some digging, though that meant that I realized I installed certain pieces wrongly and had to disassemble them

The neopixels were a bitch to install. Even now I haven't really installed them correctly as the 2 lights that were supposed to point towards the hotend just does not work. I suspect it is a wiring issue likely due to a bad crimp on my part

Overall the base kit came pretty complete and since everything is pre-crimped, you are not likely to need any special tools, though do remember to get your own locktite as it did not come with it. The other thing that is missing in the base kit would be a 4x3 PTFE tube. I initially had many printing issues. I had issues where the prints would constantly fail. It had bed adhesion issues, it would stop extruding midway thru the print. It would have inconsistent extrusions, etc

Here were my general learnings on why this had happened
- Nozzle was too close to the bed. It needs a bit more space to work with, this is quite easy to tell. If it is too close you would be able to hear your nozzle dragging on the build plate or dragging along the previous print layer. This is a clear tell tale sign that you need to tweak your z offset to give it more allowance
- Not having a reverse bowden tube - I am not sure if this is because I am putting my filament into a filament dry box, and hence having a longer pathway to the tool head, but I have noticed that not having a reverse bowden tube creates a lot of drag. This is apparent in the print layers, where there were issues with layers that were closer to the front of the build plate, and I have observed the toolhead would get pulled up (my build comes with a voron tap). This problem went away as soon as I installed a 4x3 PTFE tube, which unfortunately did not come with the kit but did come with the original voron 2.4 BOM. This part was also not very clear in the documentation that it should be installed
- The last issue, which is just a guess, is that the CAN Bus wire was having connectivity issues, after I have adjusted the wire angle to reduce strain, the random extrusion stop issues seem to have gone away

On top of the base kit, I took a decision to do certain upgrades. While that meant that I had to take apart the printer again, I thought it was well worth it in various ways

The original kit came with the FYSETC Spider board and FYETC's Stealthburner CAN Toolhead board. I replaced it with BTT's manta M8P and BTT's SB2240. My first FYSETC CAN TH board was dead during installation. FYSETC was kind enough to send me a replacement at the cost of shipping only. Upon scouring the internet for issues, seems like FYSETC's SB TH board was very sensitive to being plugged/unplugged while powered and this could short the board. This was the same with their spiderboard too where under certain conditions you can damage the board. It feels like "edge case handling" isn't part of their boards' design in general

I have twice accidentally shorted BTT's boards and they came out fine in both cases. In one case I had to replace the fuse and in the other it just continued to work

FYETC boards does support CAN, however the CAN implementable assumes either that you are only connecting just 2 devices to the CAN network (the toolhead MCU and the Main MCU), or that those devices are the end devices. This is apparent from the fact that I was unable to find any jumper option to remove the 120 Ohms resistor. According to the CANBus specs, the resistor should be installed at each end of the network. With BTT's M8P and the SB2240, it comes with jumpers to allow you to add or remove the 120 ohm resistors

Also BTT's SB2240 comes with a very high quality canbus cable with a built in cable strain, which can reduce issues on connectivity

Speaking of which I do have 2 boards that I would probably never use if anybody wants. the Spider 2.0 and a Manta M8P 1.0 if anyone is interested and living in Singapore, happy to give it away

I upgraded the hotend to a Rapido v2. It does allow slightly higher flow than the stock but personally I did not feel a huge difference with this update

I swapped out the CW2 with a Galileo 2 extruder. Similarly, I did not see too much of a difference, apart from that it probably offers more torque and less backlash than the CW2

I added a filament runout sensor, the SFS 2.0 from BTT. I had some issues initially with the installation, where only the filament run out switch worked but not the encoder. It ultimately turned out to be a bad crimp on the 5v power supply. The biggest tell tale signs were that the blue light emitted was extremely dim and it did exhibit any of the given behaviors written in the documentation - Red light where no filament was inserted, blinking blue light when the filament was getting pulled through the sensor

I added in additional MCU to support the filament sensor and exhaust fan. Honestly this is probably quite a bit of over-engineering. In part I was curious about the CANBus network in general. So far I thought it was pretty cool, given the usage in the automotive industry as well and it being only a 2 wire system to connect various nodes

In order to support this, I ordered an additional BTT EBB42, as well as a BTT CEB. The installation of this was quite straightforward. Hardest piece was really creating a custom exhaust housing that would mount the EBB42 within

This also means potential future upgrades like the StealthChanger or TapChanger to add additional toolheads

The printer is looking pretty good at the moment. The next piece around it is probably to print and assemble the ECRF v2 kit that i have ordered