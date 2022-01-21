## GPIO Pins

The Nexus DR-X Pi image and the Nexus DR-X board use the following GPIO pins (BCM numbering):

| GPIO Pin (BCM) | Purpose |
| :---: | :---: |
| 12 | PTT Left Radio |
| 23 | PTT Right Radio |
| 26 | Shutdown Button |
| 24 | Shutdown Button LED |
| 25 | Piano switch position 1 |
| 13 | Piano switch position 2 |
| 6 | Piano switch position 3 |
| 5 | Piano switch position 4 |

You can test PTT operation using `raspi-gpio` in the Terminal. For example, here's how to test PTT on the left radio (GPIO BCM pin 12):

- Set BCM pin 12 as output:

		raspi-gpio set 12 op
		
- Set BCM pin 12 state to high (PTT ON):

		raspi-gpio set 12 dh

- Set BCM pin 12 state to low (PTT OFF):

		raspi-gpio set 12 dl

These commands can also be used in scripts and in certain ham radio applications that allow scripting to control PTT.

## [OPTIONAL and ADVANCED] Backing up your Pi via Secure Shell (SSH) over a network

If you have another Linux host, you can use the `ssh-image.sh` script in this repository to make an image of a running Raspberry Pi using an SSH connection.  You'll need the following for this to work:

- Some Linux and SSH experience.
- The `ssh-image.sh` script in this repository.
- The Winlink client `pat` app and the `patmail.sh` (both are installed by default) script if you want the `ssh-image.sh` script to automatically email you with the results.  This is handy of you run the script via cron.
- SSH keypair with a passphrase-less private key (not recommended) or a keychain (recommended) on your Linux host.

See the description at the beginning of the `ssh-image.sh` script for details.

## Bugs

Probably.  WATCH THIS SPACE.  I will post bug information and workarounds here.

## Annoyances

Things that aren't really bugs, but irritating nevertheless will be documented here.

