# Troubleshooting potential errors

If you are running macOS, make sure you've followed the [further setup guide](https://github.com/tbodt/ish/wiki/macOS#further-setup).

// TODO: Xcode tips and instructions

## Issues with networking/apk
If you've received an error when installing a program or running `apk update`, e.g.
```
       ERROR: http://dl-cdn.alpinelinux.org/alpine/v3.8/main: temporary error (try again later)
```
check the output of `cat /etc/resolv.conf`.

If that returns nothing, you might be on a cellular network.
Solutions to this:

1. Connect to a WiFi network so iSH can get the nameservers automatically, or set your own nameservers:
```
$ echo "nameserver 8.8.8.8" > /etc/resolv.conf
```
Now try 