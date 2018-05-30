# Installing Arch Linux to a USB Stick
---

This achieves a persistent Arch Linux install to a USB drive.

## Create a Live USB (Optional)
 * dd if=/PathToIso/ArchLinux.iso of=/dev/sdX status=progress

## Run Arch Linux Live
 * fdisk /dev/sdX
   + Create the cross-platform partition
     - n
     - Primary/Extended: p
     - Number: 1
     - Start: 22528
     - End: +#G
     - Type: b    (W95 FAT32)
     - a    1
   + Create the GNU/Linux OS partition
     - n
     - Primary/Extended: p
     - Number: 2
     - Start: <default>
     - End: +#G
     - Type: <default>
   + Create the EFI partition
     - n
     - Primary/Extended: p
     - Number: 3
     - Start: <default>
     - End: +550M
     - Type: ef
 * Create the Filesystems:
   + mkfs.fat -F32 /dev/sdX1
   + mkfs.ext4 /dev/sdX2
     - If you want to disable journaling to get slightly fewer writes, use -o "^has_journal"
   + mkfs.fat -F32 /dev/sdX3

 * Mount the Main Partitions:
   + mount /dev/sdX2 /mnt
   + mkdir /mnt/boot; mount /dev/sdx3 /mnt/boot
   + mount /dev/sdX3 /mnt/boot
 * Pacstrap the Base Arch System:
   + pacstrap /mnt base
     - You may add other packages early, delemited by spaces, after "base"
 * Mount the Shared Drive Partition:
   + mkdir /mnt/shared
   + mount /dev/sdX1 /mnt/shared
 * Generate fstab for Booting:
   + genfstab -U /mnt >> /mnt/etc/fstab
 * Chroot into the new system:
   + arch-chroot /mnt

## Chrooting into the New System
 * Setting the System Time:
   + rm /etc/localtime
   + ln -s /usr/share/zoneinfo/US/Central /etc/localtime
   + hwclock --systohc
 * Setting the Locale:
   + vi /etc/locale.gen
     - Uncomment desired locale
   + locale-gen
   + echo LANG=en_US.UTF-8 > /etc/locale.conf
 * Setting the Hostname:
   + echo `hostname` > /etc/hostname
   + vi /etc/hosts
     - 127.0.1.1 <hostname>.localdomain <hostname>

 * Make RAM Disk Image USB Bootable:
   + vi /etc/mkinitcpio.conf
     - Reset `HOOKS=(...)` line to have `block` right after `udev`
   + mkinitcpio -p linux
 * Reset Network Device Names to Defaults
   + ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules

 * Keep Journal in RAM:
   + vi /etc/systemd/journald.conf
     - Set `Storage=volatile`
     - Set `SystemMaxUse=16M`
 * Reduce Journaling:
   + vi /etc/fstab
     - Change ext4/UDF line to have `relatime` changed to `noatime`

 * Setup GRUB Bootloader:
   + pacman -S grub efibootmgr
 * Setup GRUB for BIOS:
   + grub-install --target=i386-pc --recheck /dev/sdX
 * Setup GRUB for UEFI:
   + grub-install --target=x86_64-efi --efi-directory /boot --boot-directory /boot --removable
 * Finish GRUB Configuration:
   + grub-mkconfig -o /boot/grub/grub.cfg
     - If there's a failure, zero out the drive with `dd` and start again
 * If you have to manually edit /boot/grub/grub.cfg:
   + vim /boot/grub/grub.cfg
     - Change `root=/dev/sdX#` to `root=UUID=...`, the UUID in /etc/fstab

 * Install Network Packages:
   + pacman -S ifplugd iw wpa_supplicant dialog
   + pacman -S broadcom-wl
     - This or broadcom-wl-dkms are for MacBooks
 * Install GPU Support Packages:
   + pacman -S xf86-video-ati xf86-video-intel xf86-video-nouveau xf86-video-vesa
 * Install other Packages:
   + pacman -S xf86-input-synaptics
   + pacman -S vim acpi sudo [  polkit  ]
   pacman -S w3m xorg xorg-xinit lxde wicd wicd-gtk
   + [  pacman -Rns nano  ]
   * NOTE: Run wicd via `wicd-cli` or `wicd-curses`
    - systemctl stop netctl
    - systemctl disable netctl
    - systemctl start wicd; systemctl enable wicd
   * NOTE: .xinitrc = `exec startlxde`

 * Set User Accounts:
   + passwd
   + useradd -m -G wheel <username>
   + passwd <username>
     - passwd -d <username>    if creating a user without a login password
   + visudo
      - Add user line `<username> ALL=(ALL) ALL`
      - Or add `<username> ALL=(ALL) NOPASSWD: ALL` for no sudo password

## Rebooting
 * Leave the chroot Environment:
   + exit
 * Unmount all Partitions:
   + umount -R /mnt
 * Shutdown or Reboot Device:
   + poweroff
     - You can also use `reboot now`

## Booting from New USB Install


