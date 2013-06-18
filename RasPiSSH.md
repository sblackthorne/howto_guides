# Raspberry Pi and SSH #
#### (running headless on a second machine) ####

This guide will walk you through the basic steps for setting up your Raspberry Pi to run *headless* (meaning not connected to a monitor or keyboard) on a second machine. This guide will only work on your local network, as connecting to the Raspberry Pi from outside the local network requires several additional steps (including changes to ports and routers). This process will be covered in a different guide. At the end of setting up your Raspberry Pi for SSH use, I will outline how to connect to the Raspberry Pi from a Mac OS X or similar UNIX machine. The guide below is written for Debian-based distributions such as Raspbian, Wheezy, and Occidentalis (to name a few). It assumes you have created an SD card complete with a distribution and have the appropriate Raspberry Pi tools:

* Raspberry Pi board
* SD card with operating system loaded
* Power supply (likely micro-USB to USB cable with 5v adapter or another source)
* Internet Access
* Ethernet cable and router/switch/jack to plug into

This guide also assumes that you have the ability to plug the Raspberry Pi into a monitor and keyboard to complete the basic setup. Let's begin by setting up the Raspberry Pi.

## Turning on the Raspberry Pi ##

To begin setting up your Raspberry Pi for running headless, there are some changes you need to make within your "Settings" configuration to allow access to a second machine. Here are the first steps to turning on the Raspberry Pi, before changes can be made:

* Insert the SD card with your operating system into the Raspberry Pi
* Plug in your Ethernet cable
* Plug in your keyboard to the USB port (or keyboard dongle for wireless keyboards)
* Plug in your monitor cable (HDMI is optimal)
* Plug your power supply into a wall jack or surge protector 
* Plug the micro-USB end into your Raspberry Pi

Once the power is connected, you should see a variety of blinking LED's on the Raspberry Pi. If the SD card slot is the "front" of the Raspberry Pi, and the Ethernet port the "back" of the Raspberry Pi, the LED's are in this order (from front to back):

* ACT (Green) == Lights up to indicate when the SD card is accessed *flashing*
* PWR (Red) == Lights up to indicate 3.3V power is connected *solid*
* FDX (Green) == Lights up if network adapter is a full duplex operation *solid*
* LNK (Green) == Lights up to indicate network activity (internet) *solid*
* 100 (Yellow) == Lights up only when the network connection is 100mbps (some boards mislabeled 10M) *solid*

You should see a solid red PWR light, a flashing ACT light, a flashing LNK light, and some level of activity on the FDX and 100 lights (eventually all three network connection lights are solid). If all the LED's are active, you should see a boot log on your screen. This is the machine loading your operating system and all peripherals. 

*If this is the very first time you are using your Raspberry Pi, the default username and password will still be in effect. For Raspbian/Wheezy/Occidentalis/Debian-based distributions, these will be:*
* Username: pi
* Password: raspberry

