
https://youtu.be/c9oL4RZvl6E?t=247
https://gist.github.com/robotamer/918d0f1dbfcf88e6ed8abb103d1336b6
## Installation Guide
  1. Start with a GLIBC base media and do the voidlinux setup as root
  2. Set up partitions as 256M-512M EFI and rest to a EXT4 RootFS (Will setup a zram block later)
## Post Guide
  1. Install xtools, vim, and base-devel: **HIGHLY RECOMMEND**
    
    # sudo xbps-install xtools vim base-devel

  2. Setup other repositories for firmware and possible drivers:
    
    # xi void-repo-nonfree void-repo-multilib void-repo-multilib-nonfree
    # xi intel-ucode
    
  3. Setup FSTRIM cronjob from [void docs](https://docs.voidlinux.org/config/ssd.html#periodic-trim-with-cron)
    
  5. Install dbus and elogind:
  
    # xi dbus elogind
    # sudo ln -s /etc/sv/dbus /var/service/
> You can also enable the elogind service if having issues. Dont install the dbus-elogind packages or such because they are dummy packages. DO NOT AVOID THESE
    
  6. Setup Graphics with Wayland  
    `xi linux-firmware-amd mesa-dri mesa-vaapi mesa-vdpau vulkan-loader mesa-vulkan-radeon wlr-rander`  
    `wlr-randr --output HDMI-A-1 --mode 1920x1080@143.981003`  
        >xi mesa-dri mesa-dri-32bit vulkan-loader vulkan-loader-32bit mesa-vulkan-radeon mesa-vulkan-radeon-32bit mesa-vaapi mesa-vdpau xorg-minimal xf86-amdgpu  
    
  8. **OPTIONAL** Install and set these settings up if you are doing wayland:
    
    # vim ~/.config/bash/envrc
    <------------------------------------->
    export QT_QPA_PLATFORM="wayland-egl"
    export ELM_DISPLAY="wl"
    export SDL_VIDEODRIVER="wayland"
    <------------------------------------->

 10. **OPTIONAL** Install DWL with [dependencies](https://codeberg.org/dwl/dwl#building-dwl)
    - Make sure to install from the releases page
    - Install respective development versions
    - If you get a wlroots warning, you need to install strictly that version of wlroots
 10B. **OPTIONAL** Setup this SH starting script  
```
[~/startdwl]
#!/bin/sh
dbus-run-session dwl -s ~/dwl/autostart.sh

[~/dwl/autostart.sh]
#!/bin/sh
pgrep pipewire > /dev/null && pkill pipewire
pipewire &
wlr-randr --output HDMI-A-1 --mode 1920x1080@143.981003
```      
  9. Setup pipewire-pulse from the [void docs](https://docs.voidlinux.org/config/media/pipewire.html)

  10.`# xi firefox foot`

  12. OPTIONAL: Setup flatpak and flatseal:
  
    # xi flatpak
    # flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
    # sudo reboot
    # flatpak install flatseal
  ### [ **Now Reboot** ]
    
## Desktop Guide (Install GUI Terminal and Browser!)
  1. Install fonts and emojis:
    
    # xi noto-fonts-emoji noto-fonts-ttf noto-fonts-ttf-extra
    
  2. Setup steam, lutris, wine, and gamemode:
    
    # xi steam lutris wine wine-devel wine-32bit winetricks gamemode
  
  3. Set up ESYNC as shown on [lutris docs](https://github.com/lutris/docs).
  
  4. Install ProtonUpQT and configure lutris-wine and proton-ge:
    
    # flatpak install flathub net.davidotek.pupgui2
  
  5. **OPTIONAL** Setup automatic compositing toggle with gamemode on DE's
  
    # sudo vim /usr/share/gamemode/gamemode.ini
    <------------------------------------->
    [custom]
    start=qdbus org.kde.KWin /Compositor suspend
    end=qdbus org.kde.KWin /Compositor resume
    <------------------------------------->
  
