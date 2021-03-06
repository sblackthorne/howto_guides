# Raspberry Pi and SSH #
#### (running headless on a second machine) ####

This guide will walk you through the basic steps for setting up your Raspberry Pi (RasPi) to run *headless* (meaning not connected to a monitor or keyboard) on a second machine. This guide will only work on your local network, as connecting to the Raspberry Pi from outside the local network requires several additional steps (including changes to ports and routers). This process will be covered in a different guide. At the end of setting up your Raspberry Pi for SSH use, I will outline how to connect to the Raspberry Pi from a Mac OS X or similar UNIX machine. The guide below is written for Debian-based distributions such as Raspbian, Wheezy, and Occidentalis (to name a few). It assumes you have created an SD card complete with a distribution and have the appropriate Raspberry Pi tools:

* Raspberry Pi board
* SD card with current version of a RasPi operating system loaded
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

Your Raspberry Pi will then boot into one of two screens: a graphical desktop or a command line. If you are at a command-line interface, that's great! You will be asked for your username and password.

*If you have not changed any settings on your Raspberry Pi, the default username and password will still be in effect. For Raspbian/Wheezy/Occidentalis/Debian-based distributions, these will be:*
* Username: pi
* Password: raspberry

If you are in a graphical desktop, use the **LXTerminal** icon to open an active terminal window with a command-line interface.

## Configuring the Raspberry Pi for SSH ##

Once you've entered the command-line interface, run the 'sudo raspi-config' command. This will open a utilities configuration box. In this box you can change a variety of settings for your Raspberry Pi, but for the purposes of using the Raspberry Pi headless, there are only a few settings we need to change.

First, we need to manage the way the computer boots upon start-up. Choose the "Enable Boot to Desktop" option. On the "Should we boot straight to desktop?" screen, choose "No." This will ensure that your Raspberry Pi will boot to the command-line interface, allowing you to SSH into it.

Second, we need to enable SSH for the Raspberry Pi. Under "Advanced Options," choose "A4 SSH." You want to enable SSH, so choose that option and press return. Your screen will flash back to the command-line interface, run the command, and then return to the configuration window. Press return to select "Ok" and you will return to the main setup screen. Go back into the "Advanced Options" and select "A2 Hostname." Pay attention to the hostname restrictions and change the hostname to something distinctive and memorable. The purpose of changing the hostname is to consistently identify the Raspberry Pi on the network. This will also be handy when we set up the Raspberry Pi to connect remotely from outside the local network (a future tutorial).

Another setting you can change from the 'sudo raspi-config' command is the password for your username. It can be important to change this password if you are going to be saving personal documents on your Raspberry Pi, and since most distributions come with the default password as 'raspberry,' you'll want to be a bit more creative. When you run the 'sudo raspi-config' command, the second option allows you change the password for the default user, in this case the user 'pi.' (If you choose to create an additional/different user, you will need to set one of those as the default to use this option.)

At this point, be sure you have the username and password for your Raspberry Pi handy, as you will need them every time you SSH into it from another machine. The next piece of information you will need is the IP address for the Raspberry Pi machine on your local network. 