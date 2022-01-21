# Quick Start
## Installation

__*Attention Current Nexus Users:*__ If you're already running an earlier version of the Nexus image, you have a tool available that allows you to back up the contents of your home folder to a USB stick/drive. It's located at __Raspberry > Hamradio > Backup/Restore Home Folder__. Use it to make a copy of your home folder prior to following the rest of this procedure. Then, once you're running the new image, install the __nexus-backup-restore__ script using the Updater (__Raspberry > Hamradio > Nexus Updater__) and run __Raspberry > Hamradio > Backup/Restore Home Folder__
and follow the instructions to restore the contents of your home folder from your USB stick/drive to the new image. This allows you to have your Fldigi setup, macros, etc, and other ham apps configuration on your new image without having to configure everything again.

1. Assemble [Nexus DR-X](http://wb7fhc.com/intro.html) board and install it and the Fe-Pi audio board onto the Pi.
1. The Nexus DR-X Pi image is larger than the allowed file size on GitHub, so I store the image on a Google Drive.  The Nexus DR-X Pi image is approximately 3.2 GB.  
	- [Access my Google Drive](https://drive.google.com/file/d/1gLUDK7K5ZHgNC5dPZbX27F-Rvef14tAK/view?usp=sharing) 
	- Click the __Download__ button when prompted with "Couldn't preview file...".
1. [OPTIONAL] After you've downloaded the ZIP file, verify it's integrity by running a checksum calculator program. This will tell you that you've downloaded the image that I uploaded. The SHA256 checksum for the above image is:

		f56acaa11a456f20a7151cbe9d74bfcf34a9737b602651ec67fd98003953932f
	
	- If you downloaded the above ZIP file to a Mac, run this command in Terminal in the folder where you downloaded the file:
	
			shasum -a 256 nexusdrxpi20201212.zip
		
		Your Mac may auto-unzip the ZIP file (making a `.img` file) upon downloading, but the original ZIP file should be in your downloads folder.
				
	- If you downloaded the above ZIP file to a Linux PC, run this command in Terminal in the folder where you downloaded the file:
	
			sha256sum nexusdrxpi20201212.zip
			
	- If you downloaded the above ZIP file to a Windows 10 PC, run this command in the Command Prompt window in the folder where you downloaded the file:
	
			CertUtil -hashfile nexusdrxpi20201212.zip SHA256
			
	In all cases, the checksum string returned by your command should match the checksum string above. Thanks to David Ranch, KI6ZHD, for his suggestion to add this step to the installation instructions.

1. Burn the image to your SD card. There are many ways to do this. The easiest is to download the [Balena Etcher](https://www.balena.io/etcher/) app for your OS (supports Linux, Windows, Mac). The Balena Etcher is easy to use and you don't have to unzip ZIP or `.tar.gz` files containing images prior to burning them to the microSD card.

	Alternatively, the official "Raspbian" way to burn the image is to use the [Raspberry Pi Imager](https://www.raspberrypi.org/software/). 

1. Insert the microSD card you just imaged into the Pi and power it on.
1. The easiest way to get your Pi set up on first boot-up is to connect it to a keyboard/video/mouse (KVM).  However, there is an alternative way to access your new Pi without a KVM, even before you've configured it:  

	- By default, the [VNC server](https://github.com/AG7GN/images/blob/master/README-Using_VNC_to_Operate_Remotely.md) is enabled on the Pi.  If you plug your Pi into an ethernet port on your home network and [install the VNC Viewer application](https://www.realvnc.com/en/connect/download/viewer/) on another PC or Mac or Chromebook also on your home network, you can connect to and control your new Pi using VNC Viewer from that PC or Mac or Chromebook.  
	- Once the Pi has fully booted up, open VNC Viewer on your other computer and enter `nexus.local` into the address bar at the top of the VNC Viewer window, then press __Enter__.  Follow the instructions and login with Username __pi__ and the default password __changeme__.  
	
## First Time Boot Instructions

__*PLEASE* DO THESE STEPS before seeking help!__

1. You'll notice the first time you start the Pi with this image that it immediately reboots within a few seconds of the desktop appearing.  This is expected behavior and is caused by a script that runs on first boot that resets the VNC and SSH client and server keys among other things.  This happens only at the first boot-up.  Also, the first time bootup takes a bit longer than usual because the filesystem is expanded to the size of the microSD card.

1. Connect your Pi's ethernet port to your home network or use the Pi's wifi to connect to your home network.  For WiFi:
	- Click on the network icon (just to the left of the speaker icon) on the Pi's top menu bar.  
	- Select your WiFi network from the list (NOTE: it make take a minute or 3 for the WiFi networks your Pi can see to appear in that list) and follow the instructions on the screen.
	
1. Click __Raspberry > Preferences > Raspberry Pi Configuration__, then click __Change Password__ to set your password.  Click __OK__, and __OK__ again.  

1. If the outside edge of the desktop appears cut off on your monitor or your desktop doesn't fully fill your monitor's screen, enable or disable __Overscan__ as needed to fix the problem.  

1. Change the Hostname of your Pi as desired - don't leave it set to `nexus`.  It's a good idea to include your call sign in the hostname to make it unique.  Example: __nexus-ag7gn__.  By convention, hostnames are lower case, but there's no harm in using capital letters.  You can use any name, but the only non-alphanumeric character allowed is a dash (-).

1. Click __OK__.

1. Click __Yes__ if prompted to reboot.

1. When the desktop appears, run the Updater: Click __Raspberry > Hamradio > Nexus Updater__, then, *only if prompted to do so*, re-run __Raspberry > Hamradio > Nexus Updater__.  Check __Raspbian OS and Apps__ and click __OK__.  Reboot if prompted.

1. Click __Raspberry > Hamradio > Nexus Updater__ to run the Updater.  Check the application(s) you want to update or install and click __OK__.  Some installations take a very long time.  Don't install an application unless you understand what the application is for.  __*Installing an application does not configure it*__. Consult the documentation for that application for configuration instructions.

	You can double-click on the app name in the Updater to obtain information about that app.  This will open the Chromium browser and and take you to the website for that app.

1. As you already know from the [First Time Boot Instructions](#first-time-boot-instructions), checking the __Raspbian OS and Apps__ item in the Updater will check for and install OS updates.  This is equivalent to running the following commands in a Terminal:

		sudo apt update
		sudo apt -y upgrade
		
1. Check the __Bugs__ and __Annoyances__ sections below for additional information.

## Customize the Main Menu

This is __OPTIONAL__ - only if you want to change what appears on the menu or the menu layout.

__WARNING:__ There is a long time bug in the Main Menu Editor that resets the menu settings to default when you click the __Cancel__ button.  So, *NEVER* click the __Cancel__ button!  Even if you made no changes, click __OK__ instead.

Also, be aware that if a menu, like the __Hamradio__ menu, has too many enabled items in it such that the menu grows beyond the vertical dimensions of the screen, those items at the end of the list won't appear in the menu.

FYI: If you make changes (other than it's placement/order in the menu) to a particular menu item, a new desktop file will be created in `/home/pi/.local/share/applications` and that file will be used to populate the menu even if there is a `.desktop` file with the same name in the default location `/usr/local/share/applications`. 

1. Click __Raspberry > Preferences > Main Menu Editor__.  

1. Select __Hamradio__ in the left pane.
1. Check or uncheck the applications listed in the center pane as desired.
1. Click the __Up__ or __Down__ buttons to move the selected item up or down in the menu list.  Add or remove separators in the menu list as desired.
1. Click __OK__ (*never* click __Cancel__!) when done.

If you delete a `*.desktop` file from `/home/pi/.local/share/applications` or `/usr/local/share/applications`, it won't appear as an available selection in the Main Menu Editor. Simply unchecking an item in the editor does not delete the `*.desktop` file.

