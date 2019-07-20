# QEMU Help
---

## Running a VM in Default Mode

### Load VM with CD
`qemu-system-x86_64 -boot order=d -drive file=<disk image>,format=<image format> -m <allocated RAM size> -cdrom <image>`
