---
title: linux
layout: page
permalink: /linux/
sitemap: false
---

## If you got here from google or the like, please be aware that this is for my own use, and many things in here could be out of date or not work at all.

<!-- vim-markdown-toc Redcarpet -->

* [Useful Stuff](#useful-stuff)
    * [ffmpeg](#ffmpeg)
        * [Combine video + audio](#combine-video-audio)
        * [combinar varios arquivos de media em um só no ffmpeg](#combinar-varios-arquivos-de-media-em-um-só-no-ffmpeg)
    * [vim](#vim)
    * [bash](#bash)
        * [adicionar extensão pra todos os arquivos](#adicionar-extensão-pra-todos-os-arquivos)
    * [scripts](#scripts)
        * [Generating CV (for Jekyll website) `./update_cv_pdf`](#generating-cv-for-jekyll-website-update_cv_pdf)
        * [generate pdf version of cv `./cv_pdf`](#generate-pdf-version-of-cv-cv_pdf)
        * [remove from filenames:](#remove-from-filenames)
        * [run scripts as apps](#run-scripts-as-apps)
    * [pdftk](#pdftk)
        * [combine pdf files](#combine-pdf-files)
        * [extract from pdf](#extract-from-pdf)
    * [Git](#git)
        * [Setting up Git](#setting-up-git)
        * [Remove directory](#remove-directory)
        * [Making existing folder into a local git repo](#making-existing-folder-into-a-local-git-repo)
    * [Numlock on startup](#numlock-on-startup)
    * [Formatting USB](#formatting-usb)
        * [gparted (Fat32)](#gparted-fat32)
    * [Nestopia](#nestopia)
    * [SSH](#ssh)
        * [Backup and sync with `rsync`](#backup-and-sync-with-rsync)
    * [RSYNC](#rsync)
        * [Music folder to phone](#music-folder-to-phone)
    * [Default Application](#default-application)
        * [File Manager (PCManFM)](#file-manager-pcmanfm)
* [Personal Configs](#personal-configs)
    * [Mouse:](#mouse)
    * [Touchpad:](#touchpad)
    * [Keyboard layout switch:](#keyboard-layout-switch)
* [Linux on Mac](#linux-on-mac)
    * [Fix wake up](#fix-wake-up)
    * [Fix slow wake up (Macbook lid open)](#fix-slow-wake-up-macbook-lid-open)
    * [MBP Fan](#mbp-fan)
    * [How to install Ardour](#how-to-install-ardour)
    * [I3 Backlight](#i3-backlight)
    * [Switch keyboard layout](#switch-keyboard-layout)
    * [Switch keyboard layout i3](#switch-keyboard-layout-i3)
    * [Xrandr](#xrandr)
    * [OBS Virtual Cam](#obs-virtual-cam)
    * [Problem with WiFi](#problem-with-wifi)
* [Packages](#packages)
* [Arch Install on Framework Laptop](#arch-install-on-framework-laptop)
    * [Packages to install:](#packages-to-install)
    * [tty2](#tty2)
    * [Intel drivers](#intel-drivers)
    * [Screen Resolution](#screen-resolution)
    * [Screen Tearing](#screen-tearing)
    * [Power Management](#power-management)
        * [Disable Screen Blanking](#disable-screen-blanking)
        * [screenlock](#screenlock)
    * [Appearance](#appearance)
        * [Change battery cap in BIOS](#change-battery-cap-in-bios)
    * [CPU Scaling Governors](#cpu-scaling-governors)
    * [backlight](#backlight)
    * [Git](#git)
    * [Trash Management](#trash-management)
    * [Update Pacman mirrorlist](#update-pacman-mirrorlist)
    * [Fix Wakeup](#fix-wakeup)
    * [Fix mouse lag](#fix-mouse-lag)
    * [TIPS](#tips)
        * [Keyboard Backlight: fn + space bar](#keyboard-backlight-fn-space-bar)
    * [Open Media Vault on Macbook](#open-media-vault-on-macbook)
        * [Login in PCManFM](#login-in-pcmanfm)
        * [Update Music Folder](#update-music-folder)
        * [Handle Lid and Screen Blank](#handle-lid-and-screen-blank)

<!-- vim-markdown-toc -->

---

---

# Useful Stuff

## ffmpeg

### Combine video + audio 
```
ffmpeg -i video.mp4 -i audio.wav -c:v copy -c:a aac -map 0:v:0 -map 1:a:0 output.mp4
```
### combinar varios arquivos de media em um só no ffmpeg
- criar files.txt:
```
file 'file1.mp3'
file 'file2.mp3'
etc...
```
- Run:
```
ffmpeg -f concat -safe 0 -i files.txt -c copy output.mkv
```

[Back to the top](#top)

---

## vim

- find and replace `:%s/foo/bar/g`

- delete inside * `di*`

- check orthography `z=`

- append numbers to end of line `:execute "% normal A \<C-R>=printf(\"%05d\", line(\".\"))\<CR>"`

[Back to the top](#top)

---

## bash

### adicionar extensão pra todos os arquivos
```
find . -type f -exec mv '{}' '{}'.jpg \;
```

---

## scripts

To run scripts: `chmod +x <script>` then `./<script>`

### Generating CV (for Jekyll website) `./update_cv_pdf`

```
#!/bin/bash

sed -i '14,$d' cv_pdf/cv_pdf.md ## deletes after line 14

sed -n '25,$p' cv.md > cv_temp ## copies from original from line 25 into temp file

sed -i '/Back to the top/d' cv_temp ## delete lines with 'back to the top'

line=13

sed -i -e "${line}r cv_temp" cv_pdf/cv_pdf.md ## inserts temp file into cv_pdf after line 13
```

### generate pdf version of cv `./cv_pdf`
  - have jekyll server running OR substitute to `https://otaviomk.com/cv_pdf/`

```
#!/bin/bash

TODAY1=$(date +%F)

wkhtmltopdf -s letter --footer-font-size 10 --footer-left 'Otavio Manzano Kavakama - cellist' --footer-right [page]/[topage] --footer-line http://127.0.0.1:4000/cv_pdf/ /home/omk/Storage/Insync/DMA\ BGSU\ 2019-/PORTFOLIO/Otavio_Manzano_Kavakama_CV_$TODAY1.pdf
```

[Back to the top](#top)

---

### remove from filenames:

```
#!/bin/bash

for f in *STRING_TO_BE_REMOVED*; do
    mv -- "$f" "${f/STRING_TO_BE_REMOVED/}"
done
```

### run scripts as apps
- add this to `.bashrc`

```
PATH=$PATH:$HOME/.scripts #making my scripts run without typing the whole path
```

[Back to the top](#top)

---

## pdftk

### combine pdf files

```
pdftk pdf1.pdf pdf2.pdf cat output final.pdf
```

### extract from pdf

```
pdftk file.pdf cat 3-8 output final.pdf
```

```
pdftk file.pdf cat 3 4 5 output final.pdf
```

[Back to the top](#top)

---

## Git

### Setting up Git
- Install `git`
- `git config --global user.name "USERNAME"`
- `git config --global user.email "email@example.com"`

### Remove directory 
- `git rm -r <directory>`
- `git commit -m "asdf"`
- `git push`

### Making existing folder into a local git repo

- `cd` to folder
- `git init`
- `git remote add origin <URL>`
- `git add --all`
- `git commit -m "MESSAGE"`
- `git push -u origin master`

[Back to the top](#top)

---

## Numlock on startup

- install numlockx
- add to `/etc/lightdm/lightdm.conf`

```
[Seat:*]
greeter-setup-script=/usr/bin/numlockx on
```

[Back to the top](#top)

---

## Formatting USB

### gparted (Fat32)

```
lsblk # check which disk
sudo umount /dev/sdX1
sudo parted /dev/sdX --script -- mklabel msdos
sudo parted /dev/sdX --script -- mkpart primary fat32 1MiB 100%
sudo mkfs.vfat -F32 /dev/sdX1
sudo parted /dev/sdX --script print
```

[Back to the top](#top)

---

## Nestopia

```
git clone https://aur.archlinux.org/nestopia.git
cd nestopia
makepkg -sri
```

[Back to the top](#top)

---

## SSH

- On server machine (remote):
  - `ip a` to get host address
- On local machine
  - `ssh USER@HOSTADDRESS`

`systemctl status sshd`

`sudo systemctl start sshd`
`sudo systemctl enable sshd`

### Backup and sync with `rsync`

`rsync -a --delete --quiet -e ssh /path/to/backup remoteuser@remotehost:/location/of/backup`

- `--delete` = file deleted on the source will be delete on backup
- `-e ssh` = access to remote server
- Script for the above, at `/etc/cron.daily/backup`:

```
#!/bin/sh
rsync -a --delete --quiet -e ssh /path/to/backup remoteuser@remotehost:/location/of/backup
```

MAKE IT EXECUTABLE!

[Back to the top](#top)

---

## RSYNC

### Music folder to phone

`rsync -a --delete --quiet /home/omk/Insync/manzano\@bgsu.edu/OneDrive\ Biz/Music/ /run/media/omk/android/Music`

---

## Default Application

### File Manager (PCManFM)
- Find out what's the default `xdg-mime query default inode/directory`
- If not correct, `sudo xdg-mime default pcmanfm.desktop inode/directory`
  - to find out the correct name of .desktop: `ls /usr/share/applications/ | grep NAME`

[Back to the top](#top)

---

---

# Personal Configs

## Mouse:
```
/etc/X11/xorg.conf.d/10-mouse.conf
```

```
Section "InputClass"
	Identifier "My Mouse"
	MatchIsPointer "yes"
# some curved deceleration
	Option "AdaptiveDeceleration" "2"
# linear deceleration (mouse speed reduction)
	Option "ConstantDeceleration" "2"
	Option "NaturalScrolling" "on"
	Option "AccelerationProfile" "-0.5"
	Option "AccelerationScheme" "none"
	Option "AccelSpeed" "-1"
EndSection
```

## Touchpad:
```
/etc/X11/xorg.conf.d/30-touchpad.conf
```

```
Section "InputClass"
    Identifier "touchpad"
    Driver "libinput"
    MatchIsTouchpad "on"
    Option "NaturalScrolling" "on"
    Option "Tapping" "on"
EndSection
```

## Keyboard layout switch:
```
/etc/X11/xorg.conf.d/00-keyboard.conf
```

```
Section "InputClass"
        Identifier "system-keyboard"
        MatchIsKeyboard "on"
        Option "XkbLayout" "us,br"
        Option "XkbModel" "pc105"
        Option "XkbOptions" "grp:alt_shift_toggle"
EndSection
```

on Polybar:
```
[module/xkeyboard]
type = internal/xkeyboard
blacklist-0 = num lock
blacklist-1 = caps lock

format-prefix = " "
format-prefix-underline = #0000ff

label-layout = %layout%
label-layout-underline = #0000ff

label-indicator-padding = 0
label-indicator-margin = 0
label-indicator-underline = #000044
```

[Back to the top](#top)

---

---

# Linux on Mac

---

Always run this before doing anything: `sudo pacman -Syu`

---

## Fix wake up

- Check which elements wake up laptop
```
cat /proc/acpi/wakeup
```
- Check which elements are waking up laptop by disabling it and testing
```
echo EHC1 >> /proc/acpi/wakeup
echo XXXX >> /proc/acpi/wakeup
```
- Create file .service in /etc/systemd/system/, you can name it whatever
```
nvim /etc/systemd/system/fixwakeup.service
```
- Add this content:

```
[Unit]
Description=fixwakeup

[Service]
ExecStart=/bin/bash -c "echo RP01 >> /proc/acpi/wakeup; echo RP02 >> /proc/acpi/wakeup; echo RP03 >> /proc/acpi/wakeup; echo EHC1 >> /proc/acpi/wakeup; echo EHC2 >> /proc/acpi/wakeup; echo XHC1 >> /proc/acpi/wakeup"

[Install]
WantedBy=multi-user.target
```

- Run these commands:
```
sudo systemctl daemon-reload
sudo systemctl start fixwakeup
```
- Check status:

```
systemctl status fixwakeup
```

- Make it starts after boot: 
```
sudo systemctl enable fixwakeup
```
- Reboot and check again with 
```
cat /proc/acpi/wakeup 
```

- If need to know which code means what, if a code has a pci number, check that number with the output of `lspci`

[Back to the top](#top)

---

## Fix slow wake up (Macbook lid open)

    nvim /etc/systemd/logind.conf

- Add these lines:

```
HandlePowerKey=suspend
HandleLidSwitch=suspend
```

[Back to the top](#top)

---

## MBP Fan

    sudo nvim /etc/modules

- Add these lines:

```
coretemp
applesmc
```

- Install mbpfan-git through your AUR enabled package manager (paman, octopi with yay, etc)

Run:

    sudo sensors-detect
    sudo systemctl enable mbpfan
    sudo systemctl start mbpfan

- Configure mbpfan (optional)
```
sudo nvim /etc/mbpfan.conf
```
Suggestion:

```
min_fan1_speed = 1300
max_fan1_speed = 6100
low_temp = 60  
high_temp = 64  
max_temp = 80  
polling_interval = 3
```

[Back to the top](#top)

---

## How to install Ardour

- Install cadence

- Install jack2

- Install pulseaudio-jack (for PA jack bridge)

- Run
```
sudo nvim /etc/security/limits.conf
```    
- Add:

```
@audio - rtprio 95
@audio - memlock unlimited
```

- Go to 
```
sudo nvim /etc/security/limits.d/10-gcr.conf
```
- Comment line
``` 
# @user yada yada
```
- Check if user is in audio group
  - In terminal: 
```
groups
```
- If not:
  - Add audio group: 
```
groupadd audio
```
  - Add user to audio group: 
```
usermod -aG audio $USER
```

REBOOT!!

[Back to the top](#top)

---

## I3 Backlight

- Install AUR package: macbook-lighter

- Change privileges of folder: 
```
sudo chmod -c -v a+x+w /sys/class/backlight/intel_backlight/brightness
```
- In i3 conf file, edit backlight (this is for usb keyboard without a backlight special key):

```
bindsym control+F2 exec --no-startup-id macbook-lighter-screen --inc 100 # increase screen brightness
bindsym control+F1 exec --no-startup-id macbook-lighter-screen --dec 100 # decrease screen brightness
```

- To make macbook backlight key to work:

- Install acpid
- Run: 
```
systemctl start acpi-service
systemctl enable acpi.service
```
- Run to check key code: 
```
acpi_listen 
```

(then press the special keys, code is after description)

- Run:
```
sudo vim /etc/acpi/events/bl-down
```
- Add:

```
event=video/brightnessdown BRTDN 00000087 00000000
action=macbook-lighter-screen --dec 100

event=video/brightnessup BRTUP 00000086 00000000
action=macbook-lighter-screen --inc 100
```

- Restart acpid: 
```
systemctl stop acpid.service
systemctl start acpid.service
```

[Back to the top](#top)

---

## Switch keyboard layout

- Add to this file:
```
/etc/X11/xorg.conf.d/00-keyboard.conf
```
- This:
```
Option "XkbLayout" "br,us"
Option "XkbOptions" "grp:alt_shift_toggle"
EndSection
```

[Back to the top](#top)

---

## Switch keyboard layout i3

- Follow steps above to add “br” to xorg file
- Create script i3-keyboard-layout at ~/.config/i3/scripts/
- Make executable: 
```
chmod +x <script>
```
- Add to i3 config file: 

```
bindsym $mod+z exec path/to/i3-keyboard-layout set us
bindsym $mod+x exec path/to/i3-keyboard-layout set br
bindsym $mod+space exec path/to/i3-keyboard-layout cycle us br
```

[Back to the top](#top)

---

## Xrandr

`xrandr --output LVDS1 --primary --mode 1280x800 --rate 144.00 --output HDMI1 --mode 1920x1080 --rate 60.00 --right-of LVDS1`

---

## OBS Virtual Cam

- Install https://github.com/umlaeute/v4l2loopback

- git clone ……
- cd to folder
- make && sudo make install

- Install https://github.com/CatxFish/obs-v4l2sink
```
yay -Syu obs-v4l2sink
```
- Load module
```
sudo modprobe v4l2loopback
```
- In OBS
  - Tools > v4l2
  - Select video device (here /dev/video2)
  - Start

- Run to the hug

[Back to the top](#top)

---

## Problem with WiFi

Read the info about BCM4331 on the Arch Wiki

Install linux-header, linux-lts-header and other stuff

---

---

# Packages

- timeshift-autosnap (auto snapshot when Syu)
- exa (beautify ls)
- gparted (formatting disks)
- mkinitcpio-numlock (AUR numlock on startup - check Arch Wiki)
- md-to-pdf (check [https://github.com/simonhaenisch/md-to-pdf](https://github.com/simonhaenisch/md-to-pdf) to update)
- yt-dlp, spotiflyer (spotiflyer-bin AUR)

[Back to the top](#top)

---

---

# Arch Install on Framework Laptop

Follow the script

## Packages to install:
- neovim, firefox, git, ranger, pcmanfm, timeshift(AUR), nitrogen, neofetch, xclip
- yay: `https://github.com/Jguer/yay`

## tty2 
- ctrl+alt+F2 in login screen
- NetworkManager: `nmtui`
- to create uder folders: `xdg-user-dirs-update`

## Intel drivers
- `intel-media-driver intel-gpu-tools xf86-video-intel`

## Screen Resolution
- run `cvt 1632 1088` and copy everything after **Modeline**
- `xrandr --newmode [STUFF COPIED]`
- `xrandr --addmode eDP1 [RESOLUTION_60.00]`
- `xrandr --output eDP1 --mode [RESOLUTION_60.00]`
- make changes permanent, add to `/etc/X11/xorg.conf.d/40-monitor.conf`:

```
Section "Monitor"
    Identifier "eDP1"
    Modeline .....
    Option "PreferredMode" "[RESOLUTION_60.00]"
EndSection
```

---

## Screen Tearing

- add to `/etc/X11/xorg.conf.d/20-intel.conf`

```
Section "Device"
  Identifier "Intel Graphics"
  Driver "intel"
  Option "TearFree" "true"
EndSection
```

---

## Power Management

- From Power Management
  - install `tlp powertop`
    - `systemctl enable tlp`
    - sudo tlp start
    - check tlp website
    - tlp config at `/etc/tlp.conf`
  - powertop (only as monitor):
    - `sudo powertop --calibrate`
    - `sudo powertop` to monitor

### Disable Screen Blanking

Run on startup (here, on bspwmrc):

```
xset s off -dpms &
xset s noblank &
```

[Back to the top](#top)

### screenlock
  - do `sudo nvim /etc/systemd/system/sleep@omk.service`
  - write:

```
[Unit]
Description=Lock the screen
Before=sleep.target
 
[Service]
User=%I
Type=forking
Environment=DISPLAY=:0
ExecStart=/usr/bin/i3lock -c 000000
 
[Install]
WantedBy=sleep.target
```

- run `sudo systemctl enable sleep@omk.service`

## Appearance
- gtk3, gtk4, qt6-base, qt5-base, lxappearance-gtk3, kvantum, breeze
- Get rid of fadings when switching workspaces
  - in `picom.conf`

```
...
fading = false;
fade-delta = 0;
fade-in-step = 1;
fade-out-step = 1;
...
```

### Change battery cap in BIOS

Pra acessar BIOS: F2 (Fn F2)

[Back to the top](#top)

---

## CPU Scaling Governors

- install `cpupwoer`
- enable and start cpupower.service
- for performance: `sudo cpupower frequency-set -g performance`
- for powersave: `sudo cpupower frequency-set -g powersave`

## backlight
- add to `/etc/udev/rules.d/90-backlight.rules`

```
SUBSYSTEM=="backlight", ACTION=="add", \
  RUN+="/bin/chgrp video /sys/class/backlight/%k/brightness", \
  RUN+="/bin/chmod g+w /sys/class/backlight/%k/brightness"
```

- add user to video group: `sudo usermod -a -G video $LOGNAME`
- reboot

[Back to the top](#top)

---

## Git

To be able to use same github repository as in previous computer:
- `git config --global user.email "manzano@bgsu.edu"`
- `git config --global user.name "kavotaman"`
- maybe `git init`, not sure

---

## Trash Management

- install `trash-cli`
  - commands: `trash-put [FILE]`; `trash-list`; `trash-empty`; `trash-restore`
- For PCManFM, install `gvfs`

---

## Update Pacman mirrorlist

- `sudo reflector --latest 20 --protocol https --sort rate --save /etc/pacman.d/mirrorlist`

[Back to the top](#top)

---

## Fix Wakeup

- check devices `cat /proc/acpi/wakeup`
- disable with `echo XXX >> /proc/acpi/wakeup`
  - for Framework, leave only `PWRB` (Power Button) enabled
- create .service file at `/etc/systemd/system`

```
[Unit]
Description=fixwakeup

[Service]
ExecStart=/bin/bash -c "echo PEG0 >> /proc/acpi/wakeup; echo XHCI >> /proc/acpi/wakeup; echo RP10 >> /proc/acpi/wakeup; echo TXHC >> /proc/acpi/wakeup; echo TDM0 >> /proc/acpi/wakeup; echo TDM1 >> /proc/acpi/wakeup; echo TRP0 >> /proc/acpi/wakeup; echo TRP1 >> /proc/acpi/wakeup; echo TRP2 >> /proc/acpi/wakeup; echo TRP3 >> /proc/acpi/wakeup"

[Install]
WantedBy=multi-user.target
```

Useful list

- PS2K: PS/2 keyboard
- PS2M: PS/2 mouse
- PWRB or PBTN: Power button
- LID: Laptop lid
- RP0x or EXPx: PCIE slot #x (aka PCI Express Root Port #x)
- EHCx or USBx: USB 2.0 (EHCI) chip
- XHC: USB 3.0 (XHCI) chip
- PEGx: PCI Express for Graphics slot #x
- GLAN: Gigabit Ethernet

[Back to the top](#top)

---

## Fix mouse lag

- go to `/etc/default/grub`
- add `usbcore.autosuspend=-1` to `GRUB_CMDLINE_LINUX_DEFAULT="xxx yyy asdf"`
- do `sudo grub-mkconfig -o /boot/grub/grub.cfg`
- reboot and check if `cat /sys/module/usbcore/parameters/autosuspend` gives `-1`

## TIPS

### Keyboard Backlight: fn + space bar

[Back to the top](#top)

---

---

## Open Media Vault on Macbook

- Access modem
- get device address
- insert ip on browser
- install extras: `wget -O - https://github.com/OpenMediaVault-Plugin-Developers/packages/raw/master/install | bash`
- on browser > System > omv-extras:
  - isntall docker, portainer

### Login in PCManFM

- Connect to Server > SSH
  - root, pw

### Update Music Folder

- SSH to server
- Do `rsync -a --delete -e ssh /home/omk/Insync/manzano\@bgsu.edu/OneDrive\ Biz/Music/ root@192.168.1.20:/srv/dev-disk-by-uuid-827ef6d8-6e25-4bb3-9c1b-e36c51a1dc15/Music`

### Handle Lid and Screen Blank

- on `/etc/systemd/logind.conf`
  - `HandleLidSwitch=ignore`
- on `/etc/default/grub`
  - `GRUB_CMDLINE_LINUX_DEFAULT="quiet consoleblank=100"`
  - 100 is in seconds
  - `sudo update-grub`


[Back to the top](#top)
