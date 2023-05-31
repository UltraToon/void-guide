## Installation Guide
  1. Start with a GLIBC base media and do the voidlinux setup as anon sudo
  2. Set up partitions as 256M-512M EFI and rest to a EXT4 RootFS (Will setup a zram block later)
### **[ Boot System ]**
  3. Add user and visudo it since void installer wont work
    
    
    # useradd -m -G input,audio,video,bluetooth,wheel,storage ivan
    # visudo
    
## Post Guide
  1. Install xtools, vim, and base-devel: **HIGHLY RECOMMEND**
    
    # sudo xbps-install xtools vim base-devel

  2. Setup other repositories for firmware and possible drivers:
    
    # xi void-repo-nonfree void-repo-multilib void-repo-multilib-nonfree
    # xi intel-ucode
    
  3. Setup cronjobs:
    
    
    # xi cronie
    
    # sudo vim /etc/cron.weekly/fstrim
    <------------------------------------->
    #!/bin/sh

    fstrim /
    <------------------------------------->
    
    # sudo vim /etc/cron.weekly/makewhatis
    <------------------------------------->
    #!/bin/sh
    
    makewhatis /usr/share/man
    <------------------------------------->
    
  4. Install NTP time sync:
    
    # xi NTP
    # sudo ln -s /etc/sv/ntpd /var/service/
    
  5. Install dbus and elogind:
  
    # xi dbus elogind
    # sudo ln -s /etc/sv/dbus /var/service/
    
  6. Setup graphics and Xorg: (skip xorg if wayland)
    
    # xi mesa-dri mesa-dri-32bit vulkan-loader vulkan-loader-32bit mesa-vulkan-radeon mesa-vulkan-radeon-32bit mesa-vaapi mesa-vdpau
    # xi xorg-minimal xf86-video-amdgpu
    
  7. Import bashrc from dotfiles and setup bash:
    
    # xi git
    # curl https://raw.githubusercontent.com/UltraToon/dotfiles/main/.bashrc -o ~/.bashrc
    # ~/.bashrc
    
  8. **OPTIONAL** Install and set these settings up if you are doing wayland:
    
    # vim ~/.config/bash/envrc
    <------------------------------------->
    export QT_QPA_PLATFORM="wayland-egl"
    export ELM_DISPLAY="wl"
    export SDL_VIDEODRIVER="wayland"
    export MOZ_ENABLE_WAYLAND=1 # only for firefox
    <------------------------------------->
    
    # xi kwayland # FOR KDE ONLY
    
  9. Setup pipewire-pulse from the [void docs](https://docs.voidlinux.org/config/media/pipewire.html) and install easyeffects for better mic:
  
    # xi easyeffects
    
  10. Setup flatpak and flatseal:
  
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
  
