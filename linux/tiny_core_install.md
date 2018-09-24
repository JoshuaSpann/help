# Installing Tiny Core Linux from Command Line
---

### NOTES
- The given disk in this guide is assumed to be `/dev/sda`, though your disk may be different
- To get the needed root parameters for grub, look at the disk name:
 - `sda` is the disk while `sda1` is a partition on the disk
 - Decrypt the disk numbers: `a` is `0`, `b` is `1`...
 - Decrypt the partition numbers by subtracting `1` from the original number: `3` is `2`, `1` is `0`...
 - `sda1` will become `(hd0,0)` in grub, `sdc1` will become `(hd2,0)`, `sdc2` will be `(hd2,1)`...
- User-defined variables are put in `[...]` tags where `...` is the value that you can change and what the value is
- Special keypresses are represented by `<...>` tags where `...` is the key or key-combination

### Partition the Disk
Use `fdisk -l` to list all available disks and partitions, note the *`Device`* field

Use fdisk to partition the disk: `sudo fdisk /dev/sda`
- Command: `n` to create new partition
 - Command action (e extended, p primary): `p`
 - Partition number: `1`
 - First cylinder: `<cr>`
 - Last cylinder: `+[size]M` (your desired size in MB)
- Command: `a` to set partition as bootable
 - Partition number: `1` assuming you are booting the linux filesystem on sda1
- Command: `w` to write changes to disk

Create the Filesystems with `sudo mkfs.ext4 /dev/sda1`

### Copy TinyCore Files to Disk
Create mount directories for your target disk and the live cd, then mount them:
`sudo mkdir /mnt/sda1 /mnt/cd`
`sudo mount /dev/sda1 /mnt/sda1`

If you are using a live image on a CD ROM you will mount /dev/cdrom:
`sudo mount /dev/cdrom /mnt/cd`

Make the boot and tce directories:
`sudo mkdir -p /mnt/sda1/boot/grub`
`sudo cp -p /mnt/cd/boot/* /mnt/sda1/boot/` will provide warnings, they should not be an issue
`sudo mkdir -p /mnt/sda1/tce` to create the persistent *tce* dir that holds application extensions
`sudo touch /mnt/sda1/tce/mydata.tgz` to create the backup file

### Install Grub2
If you want to use grub as a bootloader, you will have to load it first:
- `tce-load -iw grub2-multi`

Next, perform a typical grub installation:
- `sudo grub-install --boot-directory=/mnt/sda1/boot /dev/sda` will give a warning, but should successfullt install:
> `grub-install: warning: cannot open directory '/usr/local/share/locale': No such file or directory.`
> `Installation finished. No error reported.`

Configure grub:
- `sudo vi /mnt/sda/boot/grub/grub.cfg`
```
menuentry "Tiny Core" {
set root=(hd0,1)
linux /boot/vmlinuz
initrd /boot/core.gz
waitusb=2
}
default 0
timeout 2
```

### Reboot into Freshly Frugal Install
`sudo umount /mnt/sda1 /mnt/cd`
`sudo reboot now`

---
## Resources
- [Frugal Install Tiny Core Linux](http://distro.ibiblio.org/tinycorelinux/install_manual.html)
- [Topic: tiny core grub2 install](http://forum.tinycorelinux.net/index.php?topic=20756.0)
