https://youtu.be/VBBuSgn-sZ4?t=1130
https://youtu.be/c9oL4RZvl6E?t=247
https://gist.github.com/robotamer/918d0f1dbfcf88e6ed8abb103d1336b6
https://www.reddit.com/r/unixporn/comments/16e7ovn/dwl_catppuccin/
https://www.dwarmstrong.org/virtualization-void-linux/  
setup void xdg
https://www.reddit.com/r/voidlinux/comments/o74i76/pipewire_rtkit_warnings/
https://gist.github.com/Piraty/2e8c9fa86d4eb70f22efb9e0ecdda235
sudo xbps-install wlroots wlroots-devel wayland-protocols wbg wlr-randr xdg-desktop-portal-wlr
https://github.com/ublue-os/bazzite/#about--features
## Installation Guide
  1. Start with a GLIBC base media and do the voidlinux setup as root
  2. Set up partitions as 256M-512M EFI and rest to a EXT4 RootFS (Will setup a zram block later)
  3. Restart
>I recommend you also make your secondary drive XFS for fast storage
## Post Guide
  1. Install xtools, vim, and base-devel: **HIGHLY RECOMMEND**
    # sudo xbps-install xtools vim base-devel

  2. Remove sudo
```
sudo
# vim /etc/xbps.d/10-ignore.conf
<---------------->
ignorepkg=sudo
<---------------->
# xbps-remove sudo
# xi doas
# vim /etc/doas.conf
<------------------------------------------------------------->
permit setenv {PATH=/usr/local/bin:/usr/local/sbin:/usr/bin:/us
<-------------------------------------------------------------->
```

  4. Setup other repositories for firmware and possible drivers:
    # xi void-repo-nonfree void-repo-multilib void-repo-multilib-nonfree
    # xi intel-ucode
    
  5. Setup FSTRIM cronjob from [void docs](https://docs.voidlinux.org/config/ssd.html#periodic-trim-with-cron)

  6. Setup [zram](https://wiki.archlinux.org/title/Zram#Using_a_udev_rule) and **reboot**
    
  7. **Only** Install dbus and elogind:
  
    # xi dbus elogind
    # sudo ln -s /etc/sv/dbus /var/service/ (might wanna do for elogind)
    
8. Setup Graphics with Wayland  
    `xi linux-firmware-amd mesa-dri mesa-vaapi mesa-vdpau vulkan-loader mesa-vulkan-radeon wlr-rander`  
    `wlr-randr --output HDMI-A-1 --mode 1920x1080@143.981003`  
        >xi mesa-dri mesa-dri-32bit vulkan-loader vulkan-loader-32bit mesa-vulkan-radeon mesa-vulkan-radeon-32bit mesa-vaapi mesa-vdpau xorg-minimal xf86-amdgpu  
    
9. Install and set these settings up if you are doing wayland:
    ```
    # vim ~/.config/bash/envrc
    <------------------------------------->
    export QT_QPA_PLATFORM="wayland-egl"
    export ELM_DISPLAY="wl"
    export SDL_VIDEODRIVER="wayland"
    <------------------------------------->
    ```

10. Install DWL with [dependencies](https://codeberg.org/dwl/dwl#building-dwl) **also get fcft w devel**
    - Make sure to install from the releases page, do not get a git version if you hate instability.
    - If you get a wlroots warning, you need to install strictly that version of wlroots
11. Setup this SH starting script  
```
[~/startdwl]
#!/bin/sh
dbus-run-session dwl -s ~/dwl/autostart.sh

[~/dwl/autostart.sh]
#!/bin/sh
wlr-randr --output HDMI-A-1 --mode 1920x1080@143.981003
pgrep pipewire > /dev/null && pkill pipewire
pipewire &
```      
  9. Setup pipewire-pulse from the [void docs](https://docs.voidlinux.org/config/media/pipewire.html)

  10.`# xi firefox foot ffmpeg slstatus`

  12. OPTIONAL: Setup [flatpak](https://flathub.org/setup/Void%20Linux) and flatseal:
    # flatpak install flatseal

  ### [ **Now Reboot** ]
    
## Desktop Guide (Install GUI Terminal and Browser!)
  1. Install fonts and emojis:
    
    # xi noto-fonts-emoji noto-fonts-ttf noto-fonts-ttf-extra noto-fonts-cjk #japanese
    
  2. Setup steam, lutris, wine, and gamemode:
    
    # xi steam lutris wine wine-devel wine-32bit winetricks gamemode
  
  3. Set up ESYNC as shown on [lutris docs](https://github.com/lutris/docs).
  
  4. Install ProtonUpQT and configure lutris-wine and proton-ge:
    
    # flatpak install flathub net.davidotek.pupgui2
  
