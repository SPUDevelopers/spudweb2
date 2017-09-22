+++
date = "2017-05-02T12:17:33-07:00"
description = "We made a Magic Mirror for our club - here's how you can make one on your own!"
disable_comments = false
draft = true
hide_authorbox = false
thumbnail = ""
title = "Making a Magic Mirror"
author = "Michael Bryant"
+++

1. Download Raspbian from https://downloads.raspberrypi.org/raspbian_lite_latest
  - We use the lite version because we don't need all of the extra stuff in the PIXEL edition.
1. Use [this guide](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to install the image to the SD card.
1. Login using the default login:
   - User: `pi`
   - Pass: `raspberry`
1. Set up WiFi by editing `/etc/wpa_supplicant/wpa_supplicant.conf` (from [The Pi Hut](https://thepihut.com/blogs/raspberry-pi-tutorials/83502916-how-to-setup-wifi-on-raspbian-jessie-lite))
   - Open the file using `nano`.
   {{< highlight bash >}}# sudo nano /etc/wpa_supplicant/wpa_supplicant.conf{{< /highlight >}}

   - Make sure it contains the following text. Replace `NETWORK_SSID` with the SSID (name) of the WiFi network and `NETWORK_PASSPHRASE` with the passphrase for that SSID.
   {{< highlight bash >}}
   country=US
   ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
   update_config=1
   network={
     ssid="NETWORK_SSID"
     psk="NETWORK_PASSPHRASE"
   }
   {{< /highlight >}}

   - Restart the Raspberry Pi.
   {{< highlight bash >}}# sudo reboot{{< /highlight >}}
   - [Better method](https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md)
1. Weird keyboard locale issue where double quote was swapped with "@" (but single quote and 2 were normal)
   1. `ls /usr/share/X11/xkb/symbols/` lists the various keyboard layouts
   1. Find the keymapping that fits with the keyboard (most are `us`)
   1. Run command `sudo dpkg-reconfigure keyboard-configuration` and follow prompts
      - Generic keyboard, then showed a list of "English (GB)" layouts. Had to hit "Other", then "English (US)", then normal "English US" from the variants
      - `sudo reboot`
      - Alternatively, run `sudo nano /etc/default/keyboard` and change the line `XKBLAYOUT="gb"` to `XKBLAYOUT="us"`
1. Magic Mirror core code comes from [this repository](https://github.com/MichMich/MagicMirror)
   - Check the README.md file
   - Current method of installing is to run [this command](https://github.com/MichMich/MagicMirror#automatic-installer-raspberry-pi-only):
     `bash -c "$(curl -sL https://raw.githubusercontent.com/MichMich/MagicMirror/master/installers/raspberry.sh)"`
     - Installer may take a while to download all of the Node components
     - Said yes to using `pm2` for magic mirror autostarting
     - Ensure that `pm2` starts at boot (Some error message about `pm2` detected init and the selected one being different): `pm2 startup`
1. Necessary extra packages:
  - `xserver-xorg` - for graphical display
  - `x11-xserver-utils` - for preventing blanking
  - `libgtk2.0-0` - electron dependency
  - `libxtst6` - electron dependency
  - `libxss1` - electron dependency
  - `libgconf2-4` - electron dependency
  - `libnss3` - electron dependency
  - `sudo npm install -g electron` - to add to PATH
    - Said `UNMET PEER DEPENDENCY stylelint@^7.8.0` - means "compatible with" version
    - `npm install stylelint@^7.8.0` seems to work
    - `sudo pm2 startup systemd` - The install script assumes "linux" as the startup type instead of "systemd"
1. For local development, may be worth using the [Docker image](https://github.com/MichMich/MagicMirror#docker)
1. Also, for updating: https://github.com/MichMich/MagicMirror#updating-your-magicmirror
1. And configuration: https://github.com/MichMich/MagicMirror#configuration


## Side note: MagicMirror will crash when running in TTY, so trying Openbox
- Install `xinit` and `openbox`
- `cp /etc/X11/xinit/xinitrc ~/.xinitrc`
- Edit `~/.xinitrc` and add this to the end: (no blanking from https://www.raspberrypi.org/forums/viewtopic.php?f=66&t=18200)
  ```
  xset s off # don't activate screensaver
  xset -dpms # disable DPMS (Energy Star) features.
  xset s noblank # don't blank the video device
  exec openbox-session
  ```
- Automatic login instructions thanks to [this forum post](http://forums.debian.net/viewtopic.php?f=16&t=123694)
  - Edit the file `/etc/systemd/system/getty@tty1.service.d/override.conf` and add these contents:
    ```
    [Service]
    ExecStart=
    ExecStart=-/sbin/agetty --autologin pi --noclear %I $TERM
    ```
  - Add `[ "$(tty)" = "/dev/tty1" ] && exec startx -- -nocursor` to the end of user's `~/.profile`
    - Makes so cursor doesn't appear over magic mirror display (only disappeared when trying to move it)
- To modify any system settings, boot the Pi and hit Ctrl+Alt+F2 to go to a TTY, and Ctrl+Alt+F1 to go back to the magic mirror

## If enabling SSH using the default user
- Change sudo privileges:
  - `sudo rm /etc/sudoers.d/010_pi-nopasswd`
    - This file allows `pi` to perform any command with sudo without a password
    - `pi` is in `sudo` group, so sudo is still available, just with password
- `sudo passwd pi` - Enter password twice. No stars or other indicator of typing appears on screen, but it is typing.
