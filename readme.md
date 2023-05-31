## Installation Guide
  1. Start with a GLIBC base media and do the voidlinux setup as anon sudo
  2. Set up partitions as 256M-512M EFI and rest to a EXT4 RootFS (Will setup a zram block later)
  3. Add user and visudo it since void installer wont work
    
    ```
    useradd -m -G input,audio,video,bluetooth,wheel,storage ivan
    visudo
    ```
## Post Guide
  1. Setup other repositories for firmware and possible drivers
    
    ```
    sudo xbps-install void-repo-nonfree void-repo-multilib void-repo-multilib-nonfree
    ```
  2. Setup cronjobs
    
    ```
    xbps-install cronie
    sudo vim /etc/cron.weekly/fstrim
    ```
