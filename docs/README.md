# Nexus DR-X Pi Image

Version 20201212.3

Author: Steve Magnuson, AG7GN

## Prerequisites

- Raspberry Pi 3B, 3B+ or 4B.  The 2GB version of the 4B is fine.
- [Fe-Pi Audio Z Version 2 sound card](https://fe-pi.com/products/fe-pi-audio-z-v2)
- Budd Churchward's ([WB7FHC](http://wb7fhc.com/index.html)) excellent [Nexus DR-X](http://wb7fhc.com/intro.html) board. The DigiLink is no longer made.
- 16GB or greater MicroSD card ([a 32GB or larger card is best](https://raspberryinsider.com/what-the-largest-micro-sd-card-supported-the-by-raspberry-pi/)). I've found that the [SanDisk 32GB Extreme PLUS microSDHC](https://www.officedepot.com/a/products/225929/SanDisk-Extreme-PLUS-microSDHC-Memory-Card/) is very fast and reliable. Samsung and SanDisk are among the most reliable cards.
- OPTIONAL: Speakers attached to Pi's built-in audio jack or an HDMI monitor with speakers if you want to monitor the radio's TX and/or RX or use Fldigi's audio alerts feature

This image uses the default configuration for user __pi__:  
- User pi's home directory is __/home/pi__
- User __pi__ has passwordless __sudo__ privileges.  
- The desktop automatically starts without requiring a password for user __pi__.

## Default Password

The default password for user __pi__ is __changeme__.  __*PLEASE CHANGE THIS* as described below!__

## Features

- Uses the latest stable Debian 10 (Buster 10.6) Raspberry Pi OS (aka "Raspbian")

- Fldigi, Flmsg, Flamp, Flarq are installed and minimally configured to use PulseAudio and 1 or 2 radios.  You must set your call sign and name, among other things, in the Fldigi and Flmsg settings.
- Flrig is installed and configured for use with 1 or 2 radios, but it is not visible on the __Hamradio__ menu by default.  See the [Customize the Main Menu](#customize-the-main-menu) section for information on customizing the menu.
- Direwolf is installed and configured for use with PulseAudio with 1 or 2 radios.
- You'll see __RMS Gateway Manager__ in the __Hamradio__ menu.  __Most users should ignore this menu item.__ This is only needed if you want this Pi to operate as an [RMS Gateway](https://www.winlink.org/tags/gateway).  

	__*Note that operating an RMS Gateway requires that you obtain a "Sysop" account at winlink.org.*__ There are [other requirements](https://www.winlink.org/content/join_gateway_sysop_team_sysop_guidelines) as well.  If you operate the Pi as an RMS Gateway, I recommend that you don't use the Pi for any other purpose.
- There are menu items to toggle on and off TX and RX audio monitoring.  This only works if you have speakers connected to your Pi's built-in audio jack or your HDMI monitor has speakers.
- Recognizes and enables a DS3231 Real Time Clock module, if installed.
- A script is installed and enabled to restart or shutdown the Pi if the pushbutton on the board is pressed (DigiLink Rev __DS__ or [Nexus DR-X](http://wb7fhc.com/intro.html) boards only).  
	- If the button is pressed for 2 <= *t* < 5 seconds then released, the Pi will reboot.  
	- If the button is pressed for *t* >= 5 seconds then released, the Pi will shutdown. 
		- Note that newer versions of the Nexus DR-X have an LED that turns on when the button is pressed for 2 <= *t* < 5 and turns off again when the button continues to be pressed for *t* >= 5 to give you a visual cue as to when to release the button to reboot or shutdown.			  
		- Older "DigiLink" boards (prior to the [Nexus DR-X](http://wb7fhc.com/intro.html)) must have the GPIO jumper installed in the '26' position for this to work.  If you want to use GPIO 13 or 6 instead (by moving the DigiLink GPIO jumper), you can edit the `/usr/local/bin/shutdown_button.py` file and set the `use_button` variable to 13 or 6 respectively.  The [Nexus DR-X](http://wb7fhc.com/intro.html) board is hard wired to GPIO 26 for this purpose - it cannot be changed.
- Watchdog service is enabled.  If the Pi locks up, it *should* automatically reboot within 10 seconds.
- Includes a GUI called the "Updater" (__Raspberry > Hamradio > Nexus Updater__) to make it easier to install and update various ham applications.
- Supports bootup user scripting based on the lever positions of the piano switch on the [Nexus DR-X](http://wb7fhc.com/intro.html) board.  A sample user script is in `/home/pi/pianoX.sh.example`.  Here's more information about [how it works](https://github.com/AG7GN/hampi-utilities/blob/master/README.md#check-piano-script).

## New in This Version

- Latest OS (Buster 10.6) and Raspberry Pi application updates.
- Buster 10.6 has a new easy to use printer manager in __Rapsberry > Preferences > Print Settings__. The __Manage Printers__ menu item is still there and opens the CUPS web interface. __Print Settings__ is easier to work with, though. 
- Incorporates Fe-Pi sound card in Raspbian's new embrace of [PulseAudio](https://github.com/AG7GN/nexus-audio/blob/main/README.md).
- Fldigi, Flrig, Flmsg, Direwolf and pat have been updated to the latest versions.
- A new Updater, the __Nexus Updater__, has replaced __Update Pi and Ham Apps__.
- These apps are now available for installation in the __Nexus Updater__:

	- CQRLog
	- Gpredict
	- Linpac
	- QSSTV
	- Uronode
	- YAAC
	
	*Important:* Note that I have not tested these applications beyond making sure they install on the Nexus!  Also, the Updater only installs applications. It does not configure them for you. Consult the documentation for the app for information on configuring it.
	
	If you use an application that can use PulseAudio, start your application like this:
	
		PULSE_SINK=fepi-playback PULSE_SOURCE=fepi-capture name-of-application [arguments]

	This will tell PulseAudio to use the Fe-Pi card for the sound for this application.
	
