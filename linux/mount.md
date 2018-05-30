# Mount
---

## Mount `dd` Generated Image

`sudo mount -o ro,loop,offset=<partitionStartSector*512> <ddFile> /mnt`


### Optional
Create the dd file as a loop device with:  
`losetup -f`
`losetup /dev/loop0 <ddFile>`  
Also use the `-P` parameter to auto-mount the partitions for you.

Delete the loop device with:  
`losetup -d /dev/loop0`
