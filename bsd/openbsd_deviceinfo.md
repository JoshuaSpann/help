# OpenBSD Help

These commands work on OpenBSD, but may work on others such as NetBSD.

## Getting Device Info

Get generic CPU info:
`sysctl -a | grep -i cpu`

For the number of cores, look for `ncpu` option under `hw`.

Get generic CPU info:
`sysctl hw.model`

Get amount of RAM:
`sysctl -a | grep -i memory`

For the available memory, look for `limit`.
