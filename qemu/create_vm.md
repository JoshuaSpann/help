# QEMU Help
---

## Creating a Virtual Machine

### Formatting Options
- `raw`
- `qcow2`

### Create a Raw Disk Image
`qemu-img create -f <format> <image name> <file size>`
`qemu-img create -f raw image_file 4G`

For other formatting options, use `-f <option>` where *<option>* is the image type

### Converting a Disk's Image Format
`qemu-img convert -f <initial format> -O <target format> <initial image name> <new image name>`
`qemu-img convert -f qcow2 -O raw image_file.qcow2 converted_image_file.raw`
