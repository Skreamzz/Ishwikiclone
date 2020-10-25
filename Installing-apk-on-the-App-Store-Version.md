# Installing `apk` on the App Store Version
Due to Apple's restrictions on the App Store, `apk` had to be removed from the rootfs on the App Store. Thankfully it is very simple to get it back installed.
1. Run 
```
wget -qO- http://dl-cdn.alpinelinux.org/alpine/v3.12/main/x86/apk-tools-static-2.10.5-r1.apk | t
ar -xz sbin/apk.static && ./sbin/apk.static add apk-tools && rm sbin/apk.static
```
2. Profit