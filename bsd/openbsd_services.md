# OpenBSD Help

## Controlling Services

Services are controlled via `rcctl`.
The command acts fairly similar to `systemctl` on Linux:
```
# Enable xenodm
rcctl enable xenodm

# Disable xenodm
rcctl disable xenodm
```
