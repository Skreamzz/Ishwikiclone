apk is removed from the rootfs. Thankfully it is very simple to get it back installed.

1. Run
```console
wget -qO- http://dl-cdn.alpinelinux.org/alpine/v3.12/main/x86/apk-tools-static-2.10.5-r1.apk | tar -xz sbin/apk.static && ./sbin/apk.static add apk-tools && rm sbin/apk.static
# For latest apk-tools, go to http://dl-cdn.alpinelinux.org/alpine/latest-stable/main/x86/
```
2. Profit