# Linking Termux to Your Phone's Storage
---

## Internal Storage
To enable termux to access your phone's internal storage or SD card, create a symlink.
Your phone storage will show up as `/storage/emulated/0/`.

Create the Link to Internal Storage:  
`ln -s /storage/emulated/0 phone`

## SD Card
You do the same as above, but instead of `/storage/emulated/0` you access the SD card under `/storage/`.
Your number may differ, in this case my SD card shows up as `/storage/0343-1F08/`.

Create the Link to an SD Card:  
`ln -s /storage/0343-1F08 sdcard`

